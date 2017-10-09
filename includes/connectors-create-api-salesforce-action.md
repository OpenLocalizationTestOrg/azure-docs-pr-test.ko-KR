해당 시간 toodo hello 트리거에 의해 생성 되는 hello 데이터와 함께 다른 흥미로운 조건 추가 했습니다. 이러한 단계 tooadd hello에 따라 **Salesforce-가져오기 개체** 동작 합니다. 이 그러면 새 잠재 고객 만들어질 때마다 hello 데이터를 가져올 됩니다. 또한 Office 365 hello 커넥터를 사용 하 여 전자 메일에서 Salesforce-Get 개체 작업 toosend hello hello 데이터를 사용 하는 두 번째 작업을를 추가 합니다.  

tooconfigure hello이 작업, 다음 정보는 tooprovide hello 필요 합니다. Hello 새 파일에 대 한 hello 속성 중 일부에 대 한 입력으로 hello 트리거에 의해 생성 된 쉬운 toouse 데이터 임을 알 수 있습니다.

| 파일 속성 만들기 | 설명 |
| --- | --- |
| 개체 형식 |Salesforce 개체에 관심이의 hello 형식입니다. 예로 Lead, Account 등이 있습니다. |
| 개체 ID |Hello 개체에 대 한 식별자를 나타냅니다. |

1. **동작 추가** 링크를 선택합니다. 검색할 수 있는 모든 작업에 대 한 있습니다이 열립니다 hello 검색 상자 tootake를 것인지 합니다. 이 예제에서는 Salesforce 동작을 사용합니다.      
   ![Salesforce 동작 이미지 1](./media/connectors-create-api-salesforce/action-1.png)  
2. 입력 *salesforce* toosearch 관련된 toosalesforce 작업에 대 한 합니다.
3. 선택 **Salesforce-가져오기 개체** 동작 tootake hello으로 합니다.   **참고**: 있습니다 하지 않았으면 지금 이전에 Salesforce 계정을 하 여 논리 앱 tooaccess tooauthorize 메시지 표시 됩니다.    
   ![Salesforce 동작 이미지 2](./media/connectors-create-api-salesforce/action-2.png)    
4. hello **가져오기 개체** 제어 열립니다.  
5. 선택 *발생할* hello 개체 형식으로.
6. 선택 hello **개체 ID** 제어 합니다.
7. 선택 **중...**  작업에 대 한 입력으로 사용할 수 있는 토큰의 tooexpand hello 목록입니다.       
   ![Salesforce 동작 이미지 3](./media/connectors-create-api-salesforce/action-3.png)    
8. 열린 **잠재 고객 ID** 컨트롤을 선택합니다.   
   ![Salesforce 동작 이미지 4](./media/connectors-create-api-salesforce/action-4.png)     
9. Hello를 해당 hello 개체 작업은 잠재 고객의 id는이 논리 앱을 트리거한 잠재 고객의 같은 toohello 잠재 고객 ID를 검색 하는 Get을 나타내는 개체 ID 컨트롤에 포함 되었습니다 hello 잠재 고객 ID 토큰을 확인 합니다.  
   ![Salesforce 동작 이미지 5](./media/connectors-create-api-salesforce/action-5.png)  
10. 작업을 저장합니다. 설정 작업이 완료, hello Get 개체 tooyour 논리 앱 작업을 추가 했습니다. 개체 가져오기 컨트롤은 다음과 같습니다.    
    ![Salesforce 동작 이미지 6](./media/connectors-create-api-salesforce/action-6.png)  

동작 tooget 잠재 고객을 추가 하면 toodo 새로 만든 hello 잠재 고객과 관련 된 사항이 흥미로운 할 수 있습니다. 회사에서 전자 메일 toonotify 새 잠재 고객을 만들었는지 메일 그룹 toosend를 수도 있습니다. 사용 커넥터 toosend hello Office 365 전자 메일에서 Salesforce에서 새 잠재 고객 개체 hello hello 관련 정보 중 일부가 합니다.  

1. 선택 **동작 추가** 다음 입력 *전자 메일* hello 검색 컨트롤에 있습니다. 이 관련된 toosending 및 전자 메일을 수신 하는 hello 동작 toothose를 필터링 합니다.  
2. 선택 hello **Office 365 Outlook에서 전자 메일 보내기** 목록 항목입니다. 아직 만들지 않은 경우는 *연결* 는 Office 365 계정 tooyour 증명된 tooenter Office 365 자격 증명 toocreate 수 이제 it 합니다. Hello, 완료 한 후 **전자 메일 보내기** 제어 열립니다.        
   ![Salesforce 동작 이미지 7](./media/connectors-create-api-salesforce/action-7.png)  
3. 싶다는 의사를 toosend 전자 메일 tooin hello hello 전자 메일 주소를 입력 **를** 제어 합니다.
4. Hello에 **주체** 제어, 입력 *만든 새 잠재 고객* -다음 선택 hello *회사* 토큰입니다. Hello 나타납니다 *회사* Salesforce에 만들어진 hello 새 잠재 고객에서 필드입니다.  
5. Hello에 **본문** 수 제어를 원하는 텍스트 선택의 hello 본문에서 toodisplay를 입력할 수도 hello 토큰이 hello 새 잠재 고객 개체에서 선택 hello 전자 메일입니다. 예를 들면 다음과 같습니다.  
   ![Salesforce 동작 이미지 8](./media/connectors-create-api-salesforce/action-8.png)   
6. 워크플로를 저장합니다.  

이것으로 끝입니다. 논리 앱이 완료되었습니다.  

이제 논리 앱을 테스트할 수 있습니다: Salesforce에서 만든 hello 조건에 맞는 새 잠재 고객을 만듭니다.  이 연습 과정을 완료한 경우 *amazon.com*을 포함하는 전자 메일 주소를 사용하여 잠재 고객을 만들면 됩니다. 몇 초 후 논리 앱 트리거되어 야 하 고 hello 결과 유사한 toothis 보일 수 있습니다.  
![Salesforce 동작 이미지 9](./media/connectors-create-api-salesforce/action-9.png)  

