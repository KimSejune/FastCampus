170904


# Git 으로 배포하기

1. Repository를 새로 만든다.
2. Portfolio를 만드는데 안에 플젝(a, b)을 넣을때는 index.html이 존재해야하며 상대경로로 이루어져야한다.
3. terminal로 이동하여서 portfolio로 이동 후 git init,   add,  commit을 순차적으로 한다. 
4. Git remote add origin (portfolio git 주소)
5. Git checkout -b gh-pages
6. Git push origin gh-pages
7. 나의 깃주소/portfolio/a  OR 나의 깃주소/portfolio/b 로 접속한다.

> `gh-pages`로 branch를 만들어야지 git에서 배포가 가능하다
