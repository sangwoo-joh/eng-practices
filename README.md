# 구글 엔지니어링 사례 문서

구글에는 모든 언어와 모든 프로젝트를 커버할 수 있는 일반적인 엔지니어링 사례가 많습니다.
이 문서는 구글에서 많은 시간 개발하면서 겪은 다양한 모범 사례의 집단적 경험을 대신합니다.
오픈소스 프로젝트 또는 다른 조직이 이 지식의 혜택을 받을 수 있기 때문에, 가능한 경우 공개적으로 사용할 수 있도록 노력합니다.

현재 여기에는 다음과 같은 문서가 있습니다:

*   두 개의 문서로 이루어진 [구글의 코드 리뷰 가이드라인](review/index.md):
    *   [코드 리뷰어를 위한 가이드](review/reviewer/index.md)
    *   [수정 저자를 위한 가이드](review/developer/index.md)

## 용어

문서에는 구글 내부에서만 쓰이는 몇 가지 용어가 있는데, 외부 독자를 위해 여기서 명확하게 뜻을 정리합니다:

*   **CL**: "changelist"를 의미합니다. 버전 컨트롤 시스템 또는 코드 리뷰 과정에 제출된 하나의 독립적인 수정(change)을 의미합니다.
    다른 조직에서는 이것을 "수정(change)", "패치(patch)", 또는 "풀 리퀘스트(pull-request)" 라고 부르기도 합니다.
*   **LGTM**: "좋아 보입니다(Looks Good To Me)"를 뜻합니다. 
    코드 리뷰어가 CL을 승인할 때 하는 말입니다.

## 저작권

문서의 저작권은 [CC-By 3.0 License](LICENSE)을 따릅니다.
공유와 배포를 적극 권장합니다.자세한 사항은 <https://creativecommons.org/licenses/by/3.0/>를 확인하세요.

<a rel="license" href="https://creativecommons.org/licenses/by/3.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by/3.0/88x31.png" /></a>
