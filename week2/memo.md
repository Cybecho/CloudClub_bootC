이해가 덜 되는 부분이 분명히 있을 것 같아서, key question과 자료 남겨요
fedora/RHEL CoreOS에서 쓰이는 ostree가 무엇인가/장점은?
https://coreos.github.io/rpm-ostree/
https://ostreedev.github.io/ostree/#operating-systems-and-distributions-using-ostree
immutable? atomic update?
다른 Linux OS에서의 것과 비교하면?
패키지 관리자 및 스냅샷 방식, 파일시스템을 기준으로
ostree와 rpm-ostree의 차이 + 동작방식?
bootc와 rpm-ostree 기반 OS의 차이?
ostree의 어떤 점을 계승했는지
OCI를 사용함으로 인해 어떤 장점이 있는지
ostree와 OverlayFS가 혼용될텐데, 각각 어느부분에 장점을 가지는지

---

geeknews에도 몇개 있네요
https://news.hada.io/topic?id=19473
https://news.hada.io/topic?id=20479

---

Proxmox + boot C
https://www.youtube.com/watch?v=OxG_OfOH5h8&t=728s

---

* Fedora/RHEL CoreOS에서 사용되는 OSTree는 무엇이며, 어떤 장점을 제공하는가?
* OSTree의 불변성(immutable)과 원자적 업데이트(atomic update) 특성은 무엇인가?
* 다른 Linux 배포판과 비교할 때 OSTree는 어떻게 다른가?

  * 패키지 관리자 관점에서
  * 스냅샷 방식 관점에서
  * 파일 시스템 관점에서
* OSTree와 rpm-ostree의 차이점은 무엇이며, 각자의 동작 방식은 어떻게 되는가?
* bootc 기반 OS와 rpm-ostree 기반 OS의 차이점은 무엇인가?
* rpm-ostree 기반 OS는 OSTree의 어떤 점을 계승하고 있는가?
* OCI(Container Image)를 활용함으로써 얻는 장점은 무엇인가?
* OSTree와 OverlayFS가 혼용될 때, 각각의 장점은 어디에 있는가?
