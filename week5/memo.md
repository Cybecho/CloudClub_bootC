github selfhosted runner는 뭐고, 왜 쓰이는거야? 그리고 bootc와 함께 사용해보라는건데, 이것이 무엇을 의미하는거고, 왜 그래야하는거고, 무엇을 위한거야? 전반적으로 기술에대해 컨셉이 이해가 가질 않는다. bootc까지는 대충 컨셉적으론 이해했는데, 이것을 github self hosted runner와 어떻게 연관지어야하는지 이해가 안간다. 이에대해 컨셉부터 쉽게 이해할 수 있도록 보고서를 작성하라.

내가 생각하는 흐름은 다음과 같다.
내 생각의 흐름 구조를 기반으로, 유의미한 사고의 흐름 구조를 정리하라.

무언가 설명을 한다는 말투보단 말보다, 사유하듯이 무엇이 헷갈렸는지? 를통해 글을 시작하고, 글이 대부분 사유하는 말투로 적어라.

---

# bootC + github actions worlflow + Github Self Hosted Runner ?

## 무엇이 헷갈렸는가?

## github actions worlflow , Github Self hosted runner 너 도대체 뭐야..?
-> bootc 는 대충 컨셉정도가 이해는 된다고 하지만, github self hosted runner는 도대체 무엇인가?
-> 개발 경험이래야 클라이언트단의 코드만 만졌던 내 수준에서는 사실 빌드-배포 파이프라인을 이해하기에 어려웠다.
-> 그래서 사실 날먹으로 self hosted runner 과제를 하루컷? 내보려고했지만, 이거 컨셉을 이해하는것부터 어려운데..?
-> 안되겠다, 일단 이 둘의 컨셉을 '왜?' 쓰는지 정리하고, 이게 bootC와 어떻게 같이 쓰일 수 있을지 내용을 정리해봐야겠다.

---

# Github Action Workflow

## What is Github Action Workflow ?
-> 이게 무엇인지 간략하게 컨셉만 소개하고, 어떤 불편함때문에 탄생하게 되었는지 설명하라.

## Why Github Action Workflow ?
-> 예시 시나리오를 만들어 쉽게 설명하시오

## How to use Github Action Workflow ?
-> 구체적인 방법보다, 전체적인 흐름을 설명하는 방식으로 설명하라

---

# Github Self hosted runner

## What is Github Self hosted runner ?
-> 이게 무엇인지 간략하게 컨셉만 소개하고, 어떤 불편함때문에 탄생하게 되었는지 설명하라.

## Why Github Self hosted runner ?
-> 예시 시나리오를 만들어 쉽게 설명하시오

## How to use Github Self hosted runner ?
-> 구체적인 방법보다, 전체적인 흐름을 설명하는 방식으로 설명하라

---

# bootC + Github Action Workflow + Github Self Hosted Runner

## 그렇다면, bootC는 Github Action Workflow 와 Github Self Hosted Runner와 어떤 연관이 있는가?
-> bootC에대해서는 이미 알고있다는 가정하에, 이 세 개념이 어떻게 통합되어 연결될 수 있을지 간략히 소개하라.

## 이렇게 함께 쓴다면, 어떤 이점을 누릴 수 있는가?
-> 예시 시나리오를 만들어 쉽게 설명하시오

## 그렇다면, 어떤식으로 구현할 수 있는가?
-> 구체적인 방법보다, 전체적인 흐름을 설명하는 방식으로 설명하라

---

# 결론

## 이 세 기술을 굳이 함께 사용했던 이유?

## bootc 이미지 빌드부터 harbor/dockerhub registry에 push하는 것을 구현하기 위해, 이 기술들이 사용되었던 이유?

## 기대효과?