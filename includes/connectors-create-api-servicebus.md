### <a name="prerequisites"></a>필수 조건
[Service Bus](https://azure.microsoft.com/services/service-bus/) 계정이 있어야 합니다.  

Azure 서비스 버스 계정에 논리 앱을 사용 하려면 먼저 hello 논리 앱 tooconnect tooyour 서비스 버스 계정에 권한을 부여 해야 합니다. 다행히 hello Azure 포털에서 논리 앱 내에서이를 쉽게 수행할 수 있습니다.  

논리 앱 tooconnect tooyour 서비스 버스 계정 hello 단계 tooauthorize 키를 같습니다.  

1. toocreate hello 논리가 응용 프로그램 디자이너에서 연결 tooService 버스, 선택 **표시 Microsoft 관리 되는 Api** hello 드롭 다운 목록에 있습니다. 다음 입력 **서비스 버스** hello 검색 상자에 있습니다. Hello 트리거나 toouse 원하는 작업을 선택 합니다.  
    ![Service Bus 연결 이미지 1](./media/connectors-create-api-servicebus/servicebus-1.png)  
2. 하기 전에 모든 연결 tooService 버스를 만들지 않은 경우 서비스 버스 자격 증명된 tooprovide 됩니다. 이러한 자격 증명이 사용 되는 tooauthorize 여 논리 앱 tooconnect tooand 서비스 버스 계정의 데이터에 액세스 합니다. hello 서비스 버스 커넥터 hello 서비스 버스 네임 스페이스에 대 한 hello 연결 문자열이 필요합니다. 또한 **관리** 사용 권한도 필요합니다. 연결 문자열에 대 한 hello 네임 스페이스 하거나 특정 엔터티 hello 경우 포함 하는 경우 좋은 방법 tooknow `EntityPath` 매개 변수입니다. 그렇지 않으면 논리 앱에 대 한 올바른 연결 문자열이 hello 않습니다.  
    ![Service Bus 연결 문자열](./media/connectors-create-api-servicebus/connectionstring.png)
3. Hello 네임 스페이스에 대 한 연결 문자열 hello를 받은 후 hello 논리 앱의 API 연결에 사용할 수 있습니다.  
    ![서비스 버스 연결 이미지 2](./media/connectors-create-api-servicebus/servicebus-2.png)  
4. Hello 연결을 만든 했으면 이제 다른 hello로 무료 tooproceed 논리 앱에서 단계를 확인 합니다.  
    ![서비스 버스 연결 이미지 3](./media/connectors-create-api-servicebus/servicebus-3.png)   

