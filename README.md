# Dart with Linear Time Stable PD

Linear Time Stable PD[https://arpspoof.github.io/project/spd/spd.html] (SCA2020) 를 Dart에 적용.

## 사용방법 및 유의사항 
* 기존에 skeleton->setForces(torques) 으로 사용하던 부분을 skeleton->setSPDTarget(target_pose, k_p, k_d) 로 사용.
* setSPDTarget 함수를 사용하고 나서 곧바로 world->step()함수를 호출하는 것을 권장. ( setSPDTarget 함수를 사용하고 나면 mass matrix, coriolis force 등을 구하는 함수에서 틀린 결과 출력. )
* 기존에 setForces함수로 사용하던 코드도 사용 가능.
* setForces 와 setSPDTarget 혼용도 가능하나, 한 step 안에서는 한 종류만 써야함. (e.g. setForces() => step() => setSPDTarget() => step() )
* 기존 SPD 사용할 때와 비교하여 30 ~ 40 % 정도의 속도 향상 효과.
