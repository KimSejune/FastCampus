170725

# CSS3 layout
- layout의 핵심은 블록 레벨 요소들을 원하는 위치에 배열하는 것이다.
- 모바일 사용자가 데스크탑 사용자보다 많은 상황을 감안하여 화면의 크기에 따라 적절히 화면 구성을 변화시키는 반응형 웹 디자인(Responsive Web Design) 또한 모던 웹 사이트의 필수 사항이 되었다.
- CSS를 사용하여 layout을 구성할 때에 자주 사용되는 핵심 기술은 float이다. 다음은 전형적인 웹사이트의 layout이다.
  - 전체를 묶은다음에 가로, 세로 순으로 묶는다.

## 1. Header & Navigatiob Bar
- 전체적인 css를 설정해주고 header를 설정한다.

## 2. Section & Aside
- 콘텐츠의 영역을 Section, 콘텐츠에 대한 Navigation item이나 부가 정보 영역을 Aside라 한다. Section 영역은 다시 article 영역으로 구분할 수 있다.
- 이 두개의 영역은 float 속성을 사용하여 수평 정렬되는 것이 일반적이다.

## 3. footer
- footer도 고정되어 있을 필요가 있지만 본문을 가리는 것은 곤란하다. 따라서 fixed 속성을 설정해서는 않된다. fixed 속성은 스크롤이 되어도 언제나 그자리를 고수하기 때문이다.
- footer는 `absolute` 속성을 설정한다. 
  - absolute 속성은 fixed와 달리 부모나 조상 중에 static 이외의 속성이 부여된 영역을 찾아 기준을 삼는다. 이때 다른 요소가 먼저 위치를 점유하고 있어도 뒤로 밀리지 않고 덮어쓰게 된다. (이런 특성을 부유 또는 부유 객체라 한다)

