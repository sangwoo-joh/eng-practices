# 좋은 CL 설명 작성하기

CL 설명은 **뭐**가 **왜** 변했는지에 대한 공개적인 기록입니다.
버전 컨트롤 기록의 영구적인 일부분이 될 것이고, 아마도 수년에 걸쳐 리뷰어 이외의 수백명의 사람이 읽게 될 것입니다.


미래의 개발자는 CL 설명을 근거로 당신의 CL을 검색할 것입니다.
미래의 누군가는 구체적인 것은 없지만 관련된 희미한 기억으로 당신의 수정을 찾을 수도 있습니다.
모든 중요한 정보가 코드에만 있고 설명이 없으면, 당신의 CL을 찾는 일이 더 어려워집니다.


## 첫줄 {#firstline}

*   완료된 내용에 대한 짧은 요약.
*   마치 명령처럼 쓰여진 완벽한 문장.
*   다음에 빈 줄이 따름.

CL 설명의 **첫줄**은 *CL이 완료한 것이* **무엇**인지를 *분명하게* 밝히는 짧은 요약이어야 합니다.
그리고 다음에 빈 줄이 이어집니다.
첫줄은 버전 컨트롤 기록의 요약에 나타나는 것이기 때문에, 나중에 코드를 검색할 사람이 당신의 CL이 실제로 뭘 *했는지* 또는 다른 CL이랑 뭐가 다른지를 이해하기 위해서 CL 자체나 설명 전체를 읽을 필요가 없도록 충분한 정보를 담고 있어야 합니다.
즉, 첫줄은 코드 기록을 더 빠르게 훑어볼 수 있도록 독립적이어야 합니다.

첫줄을 짧고, 집중적이고, 간단명료하게 쓰도록 노력해야 합니다.
명확하고 유용하게 읽을 수 있도록 하는 것이 최고 관심사여야 합니다.

전통적으로 CL 설명의 첫줄은 마치 명령처럼 쓰여진 하나의 완벽한 문장입니다.
예를 들면, \"**Delete** the FizzBuzz RPC and **replace** it with the new system." 처럼 명령문의 형태입니다. (한글 커밋 메시지에서는 그냥 평문이어도 될 것 같은데...)
그렇지만 CL 설명의 나머지 부분을 명령형으로 쓸 필요는 없습니다.

## 유익한 본문 {#informative}

설명의 나머지 부분은 유익해야 합니다.
풀려고 하는 문제에 대한 짧은 설명을 포함하거나, 왜 이것이 최선의 접근인지를 담을 수 있습니다.
그 접근에 어떤 단점이 있다면 언급되어야 합니다.
관련이 있다면 버그 번호나 벤치마크 결과, 디자인 문서에 대한 링크와 같은 배경 정보를 담습니다.

외부 리소스에 대한 링크를 담는 경우, 접근 제한이나 보유 정책으로 나중에 접근할 수도 없다는 것을 고려해야 합니다.
가능한 경우 리뷰어와 나중에 읽을 사람이 CL을 이해할 수 있도록 충분한 문맥을 담습니다.

작은 CL 조차도 디테일에 신경 쓰는 것이 좋습니다.
CL을 이해할 수 있는 맥락을 담읍시다.


## 나쁜 CL 설명 {#bad}

"Fix bug(버그 수정)"는 부적절한 CL 설명입니다.
어떤 버그인지, 무엇을 수정했는지, 이런 내용이 빠져있습니다.
비슷하게 나쁜 설명의 예시는 다음과 같습니다:

-   "Fix build(빌드 수정)."
-   "Add patch(패치 추가)."
-   "Moving code from A to B(A에서 B로 코드 이동)."
-   "Phase 1(단계 1)."
-   "Add convenience functions(편의 함수 추가)."
-   "kill weird URLs(이상한 URL 삭제)."

이 중 몇 개는 실제 CL 설명에서 발췌했습니다.
짧긴 하지만, 충분히 유용하지 못합니다.

## 좋은 CL 설명 {#good}

좋은 설명에 대한 몇 가지 예시입니다.

### 기능 수정

> rpc: remove size limit on RPC server message freelist.
>
> Servers like FizzBuzz have very large messages and would benefit from reuse.
> Make the freelist larger, and add a goroutine that frees the freelist entries
> slowly over time, so that idle servers eventually release all freelist
> entries.

앞부분의 몇 글자는 CL이 정확히 뭘 하는지 설명합니다.
나머지 부분은 해결하려는 문제를 설명하고, 왜 이게 좋은 해결책이며, 구체적인 구현에 대한 정보를 담고 있습니다.


### 리팩토링


> Construct a Task with a TimeKeeper to use its TimeStr and Now methods.
>
> Add a Now method to Task, so the borglet() getter method can be removed (which
> was only used by OOMCandidate to call borglet's Now method). This replaces the
> methods on Borglet that delegate to a TimeKeeper.
>
> Allowing Tasks to supply Now is a step toward eliminating the dependency on
> Borglet. Eventually, collaborators that depend on getting Now from the Task
> should be changed to use a TimeKeeper directly, but this has been an
> accommodation to refactoring in small steps.
>
> Continuing the long-range goal of refactoring the Borglet Hierarchy.

첫줄은 CL이 무엇을 하는지와 과거와 어떻게 다른지 설명합니다.
나머지 부분은 구체적인 구현, 이 해결책이 이상적이지는 않다는 것을 밝히는 CL의 문맥, 그리고 가능한 미래 방향에 대해 얘기합니다.
또한 *왜* 이 수정이 이루어졌는지도 설명합니다.

### 약간의 문맥이 필요한 작은 CL

> Create a Python3 build rule for status.py.
>
> This allows consumers who are already using this as in Python3 to depend on a
> rule that is next to the original status build rule instead of somewhere in
> their own tree. It encourages new consumers to use Python3 if they can,
> instead of Python2, and significantly simplifies some automated build file
> refactoring tools being worked on currently.

첫번째 문장은 정확히 뭘 완료했는지 설명합니다.
나머지는 *왜* 이 수정이 이루어졌는지를 설명하면서 리뷰어에게 많은 문맥을 제공합니다.

## 자동으로 생성된 CL 설명

어떤 CL은 도구에 의해 생성됩니다.
가능하다면, 이렇게 생성된 CL의 설명도 여기에 있는 조언을 따라야 합니다.
즉, 첫줄은 짧고, 집중적이고, 독립적이어야 하고 CL 설명 본문은 리뷰어와 나중에 코드를 검색할 사람이 CL의 영향을 이해하는데 도움을 주는 유익한 세부 사항을 담아야 합니다.

## CL을 제출하기 전에 설명을 리뷰하기

리뷰가 진행되면서 CL은 커다란 수정을 겪을 수도 있습니다.
이럴 때는 CL을 제출하기 전에 CL의 설명이 제대로 되었는지 한번 더 확인해볼 가치가 있습니다.
이를 통해 CL이 무엇을 하는지를 설명이 잘 반영하고 있는지 확인할 수 있습니다.

다음: [작은 CL](small-cls.md)
