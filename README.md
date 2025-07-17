# GCP VM 기반 Kubernetes 클러스터에 Spring Boot 배포 프로젝트

이 프로젝트는 GKE를 사용하지 않고, Google Cloud Platform(GCP)의 Compute Engine VM에 직접 `kubeadm`을 사용하여 Kubernetes 클러스터를 구축하고, 직접 만든 Spring Boot 애플리케이션을 Docker 이미지로 빌드하여 배포하는 전체 과정을 기록한 리포지토리입니다.

## 프로젝트 구조

- `/app`: "Hello World" HTML 페이지를 제공하는 Spring Boot 애플리케이션 소스 코드
- `/kubernetes`: Kubernetes 클러스터에 배포하기 위한 YAML 매니페스트 파일
- `Dockerfile`: `/app`의 소스 코드를 Docker 이미지로 빌드하기 위한 파일 (app 폴더 내에 위치)

## 핵심 기술 스택

- **클라우드**: Google Cloud Platform (GCP)
- **구조**: Compute Engine (VM Instance)
- **사용된 기술**: Kubernetes (kubeadm), Docker, Spring Boot, Java 17, Gradle
- **CI/CD**: Docker Hub

## 실행 방법

### 1. Docker 이미지 빌드 및 푸시

로컬 컴퓨터의 `app` 폴더로 이동한 후, 아래 명령어를 실행하여 Docker Hub에 이미지를 푸시합니다. (`<username>`은 본인의 Docker Hub ID로 변경)

```bash
# AMD64 아키텍처용으로 빌드하여 푸시
docker buildx build --platform linux/amd64 -t <username>/k8s-hello:2.0 --push .
