---
layout: post
title: git 배우기
subtitle: frontier mission
header-img: img/in-post/2020-10-07/header.jpg
header-style: text
catalog: true
tags:
  - 개발
---

# git 배우기

![image.png](/img/learn_to_git/image.png)

이 사이트에서는 위에 있는 것처럼 git에 기본 명령어들을 공부 할 수 있다.
[https://learngitbranching.js.org/?locale=ko](https://learngitbranching.js.org/?locale=ko)

1. git commit : 커밋은 Git 저장소에 여러분의 디렉토리에 있는 모든 파일에 대한 스냅샷을 기록하는 것입니다.
    
    ![image.png](/img/learn_to_git/image%201.png)
    
    이런식으로 C1에서 C2로 comit이 된걸 볼 수 있습니다. 방금 저장소 내용을 변경해서 하나의 커밋으로 저장했습니다. 방금 만든 커밋은 부모는 `C1`이고, 어떤 커밋을 기반으로 변경된 것인지를 가리킵니다.
    
2. git branch : 브랜치는 특정 커밋에 대한 참조(reference)에 지나지 않습니다. 브랜치를 "하나의 커밋과 그 부모 커밋들을 포함하는 작업 내역"이라고 기억하시면 됩니다.
사용 법 : git branch [name]
분리를 했으면 합치기도 해야겠죠? 처음으로 살펴볼 방법은 `git merge`입니다. Git의 합치기(merge)는 두 개의 부모(parent)를 가리키는 특별한 커밋을 만들어 냅니다. 두개의 부모가 있는 커밋이라는 것은 "한 부모의 모든 작업내역과 나머지 부모의 모든 작업, *그리고* 그 두 부모의 모든 부모들의 작업내역을 포함한다"라는 의미가 있습니다.
    
    ![image.png](/img/learn_to_git/image%202.png)
    
    이런식으로 `git merge bugFix` 라는 명령어를 통해 branch를 합칠 수 있습니다.
    
3. git Rebase : 브랜치끼리의 작업을 접목하는 두번째 방법은 *리베이스(rebase)*입니다. 리베이스는 기본적으로 커밋들을 모아서 복사한 뒤, 다른 곳에 떨궈 놓는 것입니다. 조금 어렵게 느껴질 수 있지만, 리베이스를 하면 커밋들의 흐름을 보기 좋게 한 줄로 만들 수 있다는 장점이 있습니다. 리베이스를 쓰면 저장소의 커밋 로그와 이력이 한결 깨끗해집니다.
    
    ![image.png](/img/learn_to_git/image%203.png)
    
    이렇게 한 줄이 됩니다.
    
4. git hand : HEAD는 현재 체크아웃된 커밋을 가리킵니다. -- 다시 말하자면 현재 작업중인 커밋입니다.
    
    *상대 커밋은 강력한 기능인데, 여기서 두가지 간단한 방법을 소개하겠습니다.
    
    - 한번에 한 커밋 위로 움직이는 `^`
        
        먼저 캐럿 (^) 연산자 부터 알아보겠습니다. 참조 이름에 하나씩 추가할 때마다, 명시한 커밋의 부모를 찾게 됩니다.
        
        `main^`는 "`main`의 부모"와 같은 의미 입니다.
        
        `main^^` 는 "`main`의 조부모(부모의 부모)"를 의미합니다
        
    - 한번에 여러 커밋 위로 올라가는 `~<num>`
        
        커밋트리에서 위로 여러 단계를 올라가고 싶을 수 있습니다. `^`를 계속 입력해서 올라가는것 말고 좋은 방법이 있습니다. Git 에는 틸드 (~) 연산자가 있습니다.
        
        (~) 틸드 연산자는 (선택적) 올라가고 싶은 부모의 갯수가 뒤에 숫자가 옵니다
        
    
    > git branch -f [who] [where]을 하면 강제로 브랜치를 특정 커밋으로 이동한다.
    > 
    
5. git 작업 되돌리기 : Git에는 작업한 것을 되돌리는 여러가지 방법이 있습니다. 변경내역을 되돌리는 것도 커밋과 마찬가지로 낮은 수준의 일(개별 파일이나 묶음을 스테이징 하는 것)과 높은 수준의 일(실제 변경이 복구되는 방법)이 있는데요.
    
    Git에서 변경한 내용을 되돌리는 방법은 크게 두가지가 있습니다 -- 하나는 `git reset`을 쓰는거고, 다른 하나는 `git revert`를 사용하는 것입니다. 다음 화면에서 하나씩 알아보겠습니다.
    `git reset HEAD~1` 명령어를 사용하면
    
    ![image.png](/img/learn_to_git/image%204.png)
    
    이런식으로 되돌리기가 가능하다.
    `git revert HEAD`이 명령어를 사용하면
    
    ![image.png](/img/learn_to_git/image%205.png)
    
    이렇게 되는데 이는 되돌리려고한 커밋의 아래에 새로운 커밋이 생겼습니다. `C2`라는 새로운 커밋에 *변경내용*이 기록되는데요, 이 변경내역이 정확히 `C2` 커밋 내용의 반대되는 내용입니다.
    

## 중간 정리

- `git commit` : 현재 작업한 변경 내용을 저장소에 기록하여 하나의 커밋으로 저장한다.
- `git commit --amend` : 가장 최근에 만든 커밋의 내용이나 메시지를 수정할 때 사용한다.
- `git branch [브랜치명]` : 새로운 브랜치를 생성하거나 현재 브랜치 목록을 확인한다.
- `git branch -f [브랜치명] [위치]` : 지정한 브랜치를 원하는 커밋 위치로 강제로 이동시킨다.
- `git merge [브랜치명]` : 다른 브랜치의 작업 내용을 현재 브랜치에 병합한다.
- `git rebase [브랜치명]` : 현재 브랜치의 커밋들을 지정한 브랜치 위로 재배치한다.
- `git checkout -i [위치]` : 커밋을 선택적으로 수정, 삭제, 합치기 등을 할 수 있는 인터랙티브 모드로 이동한다.

1. cherry-pick : 
• `git cherry-pick <Commit1> <Commit2> <...>` 이렇게 사용을 합니다.
현재 위치(`HEAD`) 아래에 있는 일련의 커밋들에대한 복사본을 만들겠다는 것을 간단히 줄인 말입니다
`git cherry-pick C3 C4 C7` 처럼 명령어를 실행하면 아래와 같이 된다.
    
    ![image.png](/img/learn_to_git/image%206.png)
    

1. **Interactive Rebase :**  커밋의 순서를 바꾸거나, 합치거나, 삭제할 수 있는 편집 모드를 연다.
`git rebase -i [위치]` 이와 같은 명령어로 사용이 된다.

2. git tag : git tag [tag_name] [where] : 태그를 붙일 수 있다.

3. git descrilble :  git에는 여러분이 가장 가까운 "닻(태그)"에 비해 상대적으로 어디에 위치해있는지 *describe(묘사)*해주는 명령어가 있습니다. 이 명령어는 `git describe` 입니다!
    
    ![image.png](/img/learn_to_git/image%207.png)
    

1. git clone : 실제로 `git clone`은 원격 저장소의 복사본을 _로컬_에 생성할때 사용하는 명령어입니다.
    
    ![image.png](/img/learn_to_git/image%208.png)
    
2. git fetch : 원격 저장소_에서_ 데이터를 가져오는 방법을 배워볼 것입니다 -- 이를 위한 명령어는 `git fetch` 입니다.
    
    ![image.png](/img/learn_to_git/image%209.png)
    
    이런식으로 clone에 있던 커밋이 로컬에 저장되었습니다.
    
    `git fetch`는 두가지의 중요한 단계를 수행합니다. 사실 이 두 단계만을 진행합니다. 그것은 :
    
    - 원격 저장소에는 있지만 로컬에는 없는 커밋들을 다운로드 받습니다. 그리고...
    - 우리의 원격 브랜치가 가리키는곳을 업데이트합니다 (예를들어, `o/main`)
    
    `git fetch`는 본질적으로 _로컬_에서 나타내는 원격 저장소의 상태를 *실제* 원격 저장소의 (지금)상태와 동기화합니다.
    
3. git pull : `git pull`은 본질적으로 `git fetch`후에 내려받은 브랜치를 병합하는 과정의 단축입니다.
    
    ![image.png](/img/learn_to_git/image%2010.png)
    

1. git push :  `git push`는 _여러분의_변경을 정한 원격저장소에 업로드하고 그 원격 저장소가 여러분의 새 커밋들을 합치고 갱신하게 합니다.
    
    ![image.png](/img/learn_to_git/image%2011.png)
    

1. `git branch -u o/main foo; git commit; git push`  or `git checkout -b foo o/main; git pull` 이 두 명령어는 임의의 브랜치(위 명령어에서는 foo)가 o/main을 추격을 한다.

![image.png](/img/learn_to_git/image%2012.png)

## 느낀점

원래 git에 대해 잘 몰랐어서 잘 안썻는데 이걸 하면서 생각보다 유용하고 공동작업에 최적화 되어 있는 것 같다는 느낌을 받았다. 그리고 이렇게 실흡 형태로 구조를 보면서 할 수 있었어서 더욱 이해가 잘됬던 것 같다.

## 인증

![image.png](/img/learn_to_git/image%2013.png)

![image.png](/img/learn_to_git/image%2014.png)
