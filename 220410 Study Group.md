# 220410 Study Group / HTTP

# 1. 패킷(packet) = 소포(택배)

Data를 준비하고, IP와 Port를 써 붙여서 보낸다.

- 아이피 : 내 컴퓨터의 주소
- 포트 : 내 컴퓨터 안의 소프트웨어의 주소

※ **구체적으로는?** : 보낸다 → 공유기가 내 IP를 보고 다음 전달할 곳으로 자동으로 선택해 전달

→ 전달 → 전달 ... 전달 → 도착

※ **일어날 수 있는 문제** : 

데이터가 전송되다가 다른 경로로 보낸 데이터보다 늦게 도착해서 순서가 바뀜

데이터가 전송되다가 중간 경로의 노드가 죽음.

▷ 네트워크는 신뢰할 수 없으므로, 중요한 데이터를 보낼 땐 유실 방지 대책이 필요!

## ※ TCP / UDP

1. **TCP** : 데이터의 누락 방지, 순서 보장.
    
    클라이언트 → 서버 : SYN(나랑 연결할래?)
    
    서버 → 클라이언트 : SYN+ACK(확인해보니 SYN이네요 연결할게요)
    
    클라이언트 → 서버 : ACK(ㅇㅋ 데이터 보낼게요)
    
    서버 → 클라이언트 : 1,3번 데이터는 왔는ㄴ데 2번 데이터가 안 왔어요
    
    클라이언트 → 서버 : ㅇㅋ 다시보내줌
    
2. **UDP** : 누락, 순서 보장 없음. 빠름. (예) 고용량의 동영상 등(픽셀 한두개 누락돼도 상관없음)
    
    클라이언트 → 서버 : 데이터 1번 발사!
    
    클라이언트 → 서버 : 데이터 2번 발사!!
    
    클라이언트 → 서버 : 데이터 3번 발사!!!
    

### ※ 데이터 전송 과정

- 목적지(IP, Port), 데이터, TCP인가 UDP인가, 다음 라우터의 주소(자동으로 되기도 함)를 전송
- 다음 라우터가 전송된 것을 받아서 다음 목적지 주소를 준비하여 전송

# 2. HTTP ?

- 컴퓨터는 0, 1밖에 모름 → 알파벳 등의 글자를 **2진수**로 변환한 **코드**
    
    다 붙여서 보내면 어디서 끊어 읽는지 모름 → 문자는 **2진수 7자리**에 맞춰서 보내기로 **약속**
    
    이런 약속 : **PROTOCOL**
    
- **HTTP** : HTML 문서와 같은 리소스를 가져올 수 있게 해주는 **프로토콜(약속)**이다.
    
    *“**텍스트”*화** 된 **데이터**의 START LINE(첫 줄), HEADER(둘째 줄부터, 빈 줄 나오기 전까지)로 BODY(내용)로 **구성하기로 약속**한 것. 
    
    → 데이터(html 문서)를 데이터 누락 없이 정확한 목적지의 소프트웨어에 **전달(Response)**하고, 원하는 환경에서 **수신(Request)**하기 위함.
    

## ※ 웹 서버란? : HTTP 요청 텍스트(http Request text)가 들어오면 그에 맞는 Response(응답) 텍스트를 보내주는 프로그램.

- **REST API** : 인터넷의 데이터 송신이 구체화되고 복잡해지니까 URL이 무한히 길어짐
    
    → **URL**은 자원만 표기하고 **Method**로 행동을 구분짓기로 약속
    
- **Method** : HTTP로 **약속**된 것. → 통일된 규칙이 생겨서 어떻게 동작할지 **예측** 가능.
    
    http의 start line(제일 첫 줄)의 제일 앞에 쓰기로 약속함. 쓸 단어도 약속돼 있음.
    
    예시)
    
    1. 회원조회 : GET /members (GET ... 뭔가 조회함)
    2. 회원가입 : POST /members (POST ... 뭔가 만듬 & 서버가 뭔가 작업해줬으면 좋겠음...)
    3. 회원수정 : UPDATE /members (UPDATE ... 뭔가 바꿈 / 보통 서버의 권한으로 막아둠)
    4. 회원탈퇴 : DELETE /members (DELETE ... 뭔가 지움 / 보통 서버의 권한으로 막아둠)