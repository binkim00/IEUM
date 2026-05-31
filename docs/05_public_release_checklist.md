# 05. Public Release Checklist

Public 레포를 만들기 전에 아래 항목을 확인합니다.

## 1. 반드시 제거할 파일

- [ ] `.env`
- [ ] `.env.local`
- [ ] API Key가 들어간 설정 파일
- [ ] serviceKey가 포함된 URL
- [ ] 대용량 원본 JSON / CSV
- [ ] 이뮤지엄 원본 이미지 URL 전체 덤프
- [ ] 팀원 내부 피드백 원문
- [ ] 수정 전 PPT / 임시 파일
- [ ] 실패 로그 / 실행 로그
- [ ] 개인 정보 또는 민감 정보

## 2. 공개 가능한 파일

- [x] README.md
- [x] docs/*.md
- [x] .gitignore
- [x] .env.example
- [x] data/samples/*.json
- [x] assets/images/.gitkeep
- [x] assets/prototype/.gitkeep

## 3. README 확인

- [ ] 서비스명과 한 줄 소개가 최종 기획서와 일치하는가
- [ ] MVP와 확장 기능이 분리되어 있는가
- [ ] Figma 링크가 연결되어 있는가
- [ ] GitHub Public 레포 링크가 연결되어 있는가
- [ ] 실제 구현 범위를 과장하지 않았는가

## 4. 데이터 확인

- [ ] 전체 원본 데이터가 포함되어 있지 않은가
- [ ] 샘플 데이터에 API Key가 포함되어 있지 않은가
- [ ] 이미지 URL에 접근 키가 포함되어 있지 않은가
- [ ] 출처와 활용 목적이 문서화되어 있는가

## 5. PDF 제출 전 확인

- [ ] PDF 안의 Figma 링크가 클릭되는가
- [ ] PDF 안의 GitHub 링크가 클릭되는가
- [ ] 버튼 도형 또는 텍스트에 링크를 걸었는가
- [ ] 링크가 Private 레포가 아닌 Public 레포로 연결되는가
- [ ] 최종 PPT에서 숨김 슬라이드와 중복 슬라이드를 삭제했는가
