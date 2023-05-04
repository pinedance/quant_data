# quant_data

퀀트 투자 기본 데이터 

Github Actions을 이용하여 자동화 함 
* 데이터 다운로드
* commit & push
* build jekyll pages 

---

## 사용법

국내 ETF 정보는 양이 많아 정해진 ticker만 불러온다. ticker는 아래 google sheet로 컨트롤 한다. 

* 시트 주소 : [KOREA_ETF_TIKCERS_FOR_DATA](https://docs.google.com/spreadsheets/d/1UqlIF8aXCsRhGYPHttIgtgVDNbyUJOtOmEsM4u3q5H0/)
* 시트 이름 : TICKERS_REQ

ticker 목록을 수정하고 데이터를 바로 보고 싶을 때는 [github action](https://github.com/pinedance/quant-data-open/actions/workflows/get-commit-push2.yml)에서 수동 실행 시킨다. 

---

## 제공하고 있는 데이터

상장 주식 목록
* 전체 [table](https://pinedance.github.io/quant-data-open/dist/CompanyList.html), [json](https://pinedance.github.io/quant-data-open/dist/CompanyList.json)

국내 ETF 가격(종가)
* 전체 [table](https://pinedance.github.io/quant-data-open/dist/KRX/etf-price.html)
* 일부 [table](https://pinedance.github.io/quant-data-open/dist/KRX/etf-price-selected.html)

경기종합지수
* 동행지수 [table](https://pinedance.github.io/quant-data-open/dist/CompositeIndex/CoincidenceIndex.html), [json](https://pinedance.github.io/quant-data-open/dist/CompositeIndex/CoincidenceIndex.json)
* 동행지수 순환변동치 [table](https://pinedance.github.io/quant-data-open/dist/CompositeIndex/CoincidenceIndexCyclicalComponent.html), [json](https://pinedance.github.io/quant-data-open/dist/CompositeIndex/CoincidenceIndexCyclicalComponent.json)
* 선행지수 [table](https://pinedance.github.io/quant-data-open/dist/CompositeIndex/LeadingIndex.html), [json](https://pinedance.github.io/quant-data-open/dist/CompositeIndex/LeadingIndex.json)
* 선행지수 순환변동치 [table](https://pinedance.github.io/quant-data-open/dist/CompositeIndex/LeadingIndexCyclicalComponent.html), [json](https://pinedance.github.io/quant-data-open/dist/CompositeIndex/LeadingIndexCyclicalComponent.json)

---

## 공공 데이터

[e-나라지표](http://www.index.go.kr)
* [수출입동향](http://www.index.go.kr/potal/main/EachDtlPageDetail.do?idx_cd=1066)

[국가통계포털 kosis](https://kosis.kr/)

[한국거래소 KRX](http://www.krx.co.kr)
* [정보데이터 시스템](http://data.krx.co.kr/)
* [보도자료](http://open.krx.co.kr/contents/OPN/05/05000000/OPN05000000.jsp): 신규상장 정보 등

산업통산자원부
* [수출입 동향](https://www.motie.go.kr/search/search.do?site=main&kwd=%EC%9B%94+%EC%88%98%EC%B6%9C%EC%9E%85+%EB%8F%99%ED%96%A5&category=c2&reSrchFlag=&currentPage=1&detailSearch=&srchFd=%24param.srchFd&sort=r&date=%24param.date&start-date=&end-date=&preCondi=%24param.preCondi&rowPerPage=10&fdTot=%24param.fdTot&fdTitle=%24param.fdTitle&fdContent=%24param.fdContent&fdFile=%24param.fdFile&fdNotice=%24param.fdNotice&ppkFlag=weekly&searchOption=allword&searchRange=fdTot&searchOptionAnd=&searchOptionOr=)
* [산업통계 분석시스템 ISTANS](https://www.istans.or.kr/mainMenu.do): [경기종합지수](https://www.istans.or.kr/su/newSuTab.do?scode=S99)
* [무역통계 k-stat](https://stat.kita.net/stat/kts/sum/SumImpExpTotalList.screen)
* [분야별통계사이트 링크](http://www.motie.go.kr/motie/py/sa/staticsitee/staticsite.jsp)

한국은행
* [경제통계시스템](https://ecos.bok.or.kr/): 통화량M2, 생산자물가지수, 소비자물가지수, 부동산 가격지수, 경제심리지수, 뉴스심리지수

[Company Guide 기업정보](https://comp.fnguide.com)

[금융토자협회 전자공시 시스템](https://dis.kofia.or.kr/)
* [펀드 다모아](https://dis.kofia.or.kr/websquare/index.jsp?w2xPath=/wq/damoa/DISFundAnnFundUnit.xml&divisionId=MDIS08006000000000&serviceId=SDIS08006000000)
* [펀드공시](https://dis.kofia.or.kr/websquare/index.jsp?w2xPath=/wq/fundann/DISFundAnnSrch.xml&divisionId=MDIS01001000000000&serviceId=SDIS01001000000)

[Fn가이드 인덱스](http://www.fnindex.co.kr/)
* [FnIndex](http://www.fnindex.co.kr/overview/I/MIS)
* [WiseIndex](https://www.wiseindex.com/Index/Index#/WMI500)

[네이버 금융](https://finance.naver.com/sise/etf.naver)

---

## 기술 기록

jekyll을 통해 json file을 변환할 때 아래와 같은 문제가 발생하였다. 각각 다음과 같이 해결하였다. 

* build 결과 파일 확장자 문제 ( filename.json.md → filename.json.html )
  - page header에 `permalink: "/filename.json"` 추가
* build 결과 파일에 html `<p>` tag가 추가되는 문제
  - `layouts/json.html`에 `{{ content | remove: "<p>" | remove: "</p>" }}` 추가
* build 결과 파일에 따옴표 문제 (`“ .. ”`)
  - kramdown의 smart quotes 기능 끄기 : `_config.yml`에 `smart_quotes: ["apos", "apos", "quot", "quot"]` 추가