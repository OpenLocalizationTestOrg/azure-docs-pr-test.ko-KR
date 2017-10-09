Hello 트리거에 의해 생성 되는 hello 데이터로 흥미로운 사항이 시간 toodo 해당 트리거를 추가 했습니다. 이러한 단계 tooadd는 hello에 따라 **SFTP-추출 폴더** 동작 합니다. 정의 된 hello 조건이 충족 될 경우이 작업에서 파일의 내용을 hello를 추출 합니다. 

tooconfigure hello이 작업, 다음 정보는 tooprovide hello 필요 합니다. Hello 새 파일에 대 한 hello 속성 중 일부에 대 한 입력으로 hello 트리거에 의해 생성 된 쉬운 toouse 데이터 임을 알 수 있습니다.

| SFTP - 폴더 압축 풀기 속성 | 설명 |
| --- | --- |
| 원본 보관 파일 경로 |Hello 파일 압축을 풀에 대 한 hello 경로입니다. 이전 작업에서 hello 토큰 중 하나를 선택 하거나 hello SFTP 서버 toofind hello 파일 경로 찾아볼 수 있습니다. |
| 대상 폴더 경로 |Hello 추출 된 파일을 저장할 hello 경로입니다. Hello 대상 경로로 이전 작업에서 hello 토큰 중 하나를 선택 하 고 또는 hello SFTP 서버를 탐색 하 고, 경로 선택 수 있습니다. |
| 덮어쓰기 |경우 hello로 파일 이름과 같은 이름을 여부 hello 기존 파일을 덮어써야 하면 hello 추출한 파일 hello 대상 폴더 경로에서 찾을 수를 나타냅니다. |

이제 시작 하겠습니다 앞에서 정의한 hello 조건이 너무 평가 되 면 hello 동작 tooextract hello 파일 추가*True*합니다. 

1. **작업 추가**를 선택합니다.        
   ![SFTP 동작 조건 이미지 6](./media/connectors-create-api-sftp/condition-6.png)   
2. 선택 hello **SFTP-추출 폴더** 동작      
   ![SFTP 동작 조건 이미지 7](./media/connectors-create-api-sftp/condition-7.png)   
3. **원본 보관 파일 경로**를 선택합니다.              
   ![SFTP 동작 조건 이미지 9](./media/connectors-create-api-sftp/condition-9.png)   
4. 선택 hello **파일 경로** 토큰입니다. 이 트리거로 hello 소스 보관 파일 경로 찾을 hello hello 파일의 hello 파일 경로 사용 함을 나타냅니다.           
   ![SFTP 동작 조건 이미지 10](./media/connectors-create-api-sftp/condition-10.png)   
5. **대상 폴더 경로**를 선택합니다.           
   ![SFTP 동작 조건 이미지 11](./media/connectors-create-api-sftp/condition-11.png)   
6. 선택 hello **파일 경로** 토큰입니다. 이 트리거 hello 추출 된 파일에 대 한 hello 대상 경로로 찾을 hello hello 파일의 hello 파일 경로 사용 함을 나타냅니다.   
7. 입력 *\ExtractedFile* hello에 **대상 폴더 경로** 제어 합니다. Hello 대상 폴더 경로 컨트롤의에서 hello 파일 경로 토큰 뒤에이 작업을 수행 합니다.         
   ![SFTP 동작 조건 이미지 12](./media/connectors-create-api-sftp/condition-12.png)   
8. 입력 *True* hello에 **덮어쓰기?* hello hello 이름이 있는 경우 기존 파일을 덮어쓴 있어야 제어 tooindicate 압축을 푼 파일입니다.      
   ![SFTP 동작 조건 이미지 13](./media/connectors-create-api-sftp/condition-13.png)   
9. Hello 변경 tooyour 워크플로 저장  

