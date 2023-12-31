# Parsing_Check.py

## Description
모바일 App 버전 ParsingCheck 입니다. <br />

1) SiteInfoCreate.py <br />

- 실행 시, SiteInfo.txt 파일에 자동적으로 현재 정상 작동중인 사이트의 SiteId와 주문리스트url을 DB에 불러와 저장합니다. <br />
(초기화 후 다시 쓰는거라 잘못누르면 초기화됨) <br />

2) SiteInfoMod.py  <br />

- 실행 시, SiteInfo.txt 파일에 Siteid 와 주문리스트 url 옆에 로그인을 위해 필요한 정보( ID, PW, login xpath) 등을
수정할 수 있습니다. <br />

3) Parsing_Check.py (메인 파일) <br />

- 실행 시에, SiteInfo.txt 파일에 있는 모든 사이트를 순차적으로 검사합니다. <br />

- 구체적으로 21 과 22 의 DB 파싱데이터가 제대로 파싱되는 건지 셀레늄을 활용하여서 검사하도록 합니다. <br />

## 실행방법:
0) 필수 모듈 설치: <br />
-pip install selenium <br />
-pip install requests <br />
-pip install chromedriver-autoinstaller <br />

1) App 테스트 할 시, SiteInfo.txt 파일에 원하는 사이트의 정보를 나열한다. (이 때, 원하지 않은 사이트는 앞에 
   #을 붙여준다.) <br /> -사이트 정보 참고 파일: DataSave1.txt <br />
   PC 테스트 할 시, SiteInfo_PC.txt 파일에 원하는 사이트의 정보를 나열한다. (이 때, 원하지 않은 사이트는 앞에 
   #을 붙여준다.)  <br /> -사이트 정보 참고 파일: DataSave1_PC.txt

2) Run Parsing_Check.py

3) Input device type (App or PC) 

4) 자동적으로 드라이버 창 화면이 뜨며, 파싱 데이터 테스트가 진행된다. <br />
    -Captcha, Bot protection 의 경우는 직접 눌러준다. (explicity wait 적용됨)

5) 프로그램 종료 후, log 폴더에 현재 시간과 Device Type 으로 저장된 로그 파일을 참고한다.
    -사이트 정보가 리스트 형태로 출력<br />
    -순서대로 파싱하고자하는 객체 이름, 파싱된 개수, 파싱된 객체 리스트 출력<br />

## Error 에 대한 설명:

* E1: SiteInfo.txt 파일에 있는 사이트 정보 중 무언가가 잘못되어서 주문내역을 열지 못하는 경우 (전체 Error) <br />
* E2: SiteInfo.txt 파일에 있는 사이트 정보 중 로그인 정보가 잘못되어서 로그인이 불가능한 경우 (go, after도 포함) <br />
* E3: 에러가 발생한 그 Key(파싱하고자 하는 객체)가 파싱이 불가능한 경우 (E6인 상황 제외) <br />
* E4: 주문리스트에서 주문상세로 넘어갈 때, detail_url 이 없어서 못넘어가는 것을 표시 <br />
* E5: 주문리스트에서 주문상세로 넘어갈 때, 주어진 detail_url로 접속했지만, 잘못된 사이트로 접속하였을 경우, DOM 을 클릭하도록 우회한다. <br />
* E6: 에러가 발생한 그 Key(파싱하고자 하는 객체)의 파싱 데이터가 잘못되어 파싱이 불가능한 경우 <br />
* E7: 주문리스트에서 주문상세로 넘어갈 때, 주어진 detail_url로 접속을 시도하였지만 접속이 불가능한 경우, DOM 을 클릭하도록 우회한다. <br />
* E8, E8A: 주문리스트에서 주문상세로 넘어갈 때, DOM 을 클릭하도록 우회했지만, 이것도 실패했을 경우 (최종 Error) <br />

## SiteInfo.txt 의 사이트 정보에 대한 설명:
->순서는 다음과 같다. <br />

사이트번호 || 사이트 url || 로그인 이메일 || 로그인 비밀번호 || 이메일 입력 xpath || 비밀번호 입력 xpath || <br />
이메일 전송 xpath || 비밀번호 전송 xpath(없을 경우 0) || gobutton: 로그인 화면으로 접속하기 위한 버튼 xpath(없을 경우 0) || <br />
afterbutton: 로그인 후, 주문리스트로 접속하기 위한 버튼 xpath(없을 경우 0) || popup_num: 로그인 전 팝업 없앨 경우 1 입력(없을 경우 빈칸) <br />
