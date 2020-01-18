# Tetris_YongjunKwon
Originals 권용준 테트리스 설계

# 설계

### 게임 외부 설계 방안

**게임 시작 화면** —> **START 버튼 클릭** —> **게임 화면**

**게임 화면** —> **게임 진행**(내부 설계 따로 기술) —> **게임 클리어** 조건 달성 : 게임 클리어 화면

                                                                           —> **게임 실패** 조건 달성 : 게임 오버 화면

**게임 클리어 조건** : Score 의 값이 40 이상 (요구 사항의 40줄 이상 조건 달성)

**게임 실패 조건** : 맨 위에 닿으면 Score가 -1이 되게 설정 —> Score의 값이 -1이하

### 게임 내부 설계 방안

게임 시작 시 GameMap 생성 —> 

## <start 클래스> //게임 시작 화면

void start(); //게임 클래스 생성하며 start 클래스는 destroy 하는 방식이 좋을듯 함

## <game 클래스> //게임 전체화면

gameMap gameMap; //게임 맵 생성
int score; //점수 생성
tetromino tetromino_temp; //다음 테트리스칸 생성

score = gameMap.get_Score;
스코어로 판단?

## <pause 클래스> //게임 포즈 화면

void onButtonClickedResume(); //재개 버튼 클릭 시 기존 게임 계속 진행
void onButtonClickedRestart(); //재시작 버튼 클릭 시 새 게임 시작(기존 객체들을 삭제하고 다시 새로 생성해야될 것인가?)

## <gameMap 클래스> //게임 화면 중 맵화면만 생각

int score; //블럭을 총 40줄 지우면 게임 완료 >>줄을 지운 점수
int map[10][20]; //0(빈칸),1(차있는칸),2(새로들어온테트로미노)
tetromino tetromino; //테트로미노 생성

void create_Tetromino(gameMap map, tetromino temp); //맵의 가장 위에 temp(다음 나올 블럭)를 생성
void clear_Line(gameMap map); //한 가로 10칸의 줄이 다 차면 줄 삭제
void fail_Game(); //블럭이 쌓여서 가장 윗줄에 닿으면 게임 종료인 것을 알림
void clear_Game(); //블럭을 총 40줄 지우면 게임 클리어 화면이 출력된다.
int get_Score(); // 게임 화면의 score 부분을 표시하기 위함
void stick_tetromino(gameMap map); //테트로미노 고정(생각으로는 배열에서 2(새로들어온테트로미노) 아래에 1(차있는 칸)이 있는 것이 확인된 지 0.5초 뒤에 2를 모두 1로 변환도 함))
void pause(); //게임을 중간에 멈춤(새로운 화면을 띄워 일시정지 한다면 기존 게임을 어떻게 멈춰두고 저장해둘 것인가?)
void auto_move(); //1초마다 현재 가진 테트로미노(배열에서 2를 차지하고 있는 칸들을 한칸씩 내림.)

## <tetromino 클래스>

테트로미노의 모양을 어떻게 저장? 배열? 회전했을 때 정보도 저장??

void create(); //테트로미노 7가지 중 랜덤적으로 생성
void rotate(); //Z키 입력 시 회전
///////////void moveAutoDown(); //테트리미노는 1초에 한 칸 밑으로 이동한다. (필요 없을 것 같음. 게임맵에서 1초단위로 moveDown 호출)
void moveLeft(); //방향키 좌측 방향 입력 시 좌측 1칸 이동
void moveRight(); //방향키 우측 방향 입력 시 우측 1칸 이동
void moveDown(); //방향키 아래 방향 입력 시 아래 1칸 이동
void moveBottom(); //Space바 입력 시 가능한 가장 밑으로 이동

고정확인은 맵?테트로미노?

// 템플릿 메소드 패턴 → 테트리미노 모양별로 다른 회전.

//회전 로직??

//화면 refresh
