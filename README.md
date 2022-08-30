# **데이터 청년 캠퍼스 _ 상명대학교**
* 3조 팀원 : 김대환, 김현재, 남유진, 윤이상, 조아현 
* 3조 주제 : 기업 정보를 활용한 중소기업 도산위험 스코어링을 통해 위험도가 높은 기업에 대한 지원정책 탐구
## 목차

* [1. 데이터 수집](#데이터-수집)
  * [1-1. 국민연금 사업장 데이터와 기업코드 병합](#국민연금-사업장-데이터와-기업코드-병합)
  * [1-2. 기업 개황 api를 이용하여 데이터 정제하기](#기업-개황-api를-이용하여-데이터-정제하기)
  * [1-3. 워크넷에서 재무제표와 사업자등록번호 가져오기](#워크넷에서-재무제표와-사업자등록번호-가져오기)
  * [1-4. dart에서 사업자등록번호 가져오기](#dart에서-사업자등록번호-가져오기)
  * [1-5. 사업자등록번호를 통해 폐업 여부 조회하기](#사업자등록번호를-통해-폐업-여부-조회하기)
  * [1-6. 필요한 변수만 남기기](#필요한-변수만-남기기)
  * [1-7. 캐치에서 기업형태 및 산업군 가져오기](#캐치에서-기업형태-및-산업군-가져오기)
  * [1-8. 잡플래닛에서 기업형태 및 산업군 가져오기](#잡플래닛에서-기업형태-및-산업군-가져오기)
  * [1-9. dart에서 상세주소 가져오기](#dart에서-상세주소-가져오기)
  * [1-10. 카카오맵 api를 통한 위도 및 경도 찾기](#카카오맵-api를-통한-위도-및-경도-찾기)
  * [1-11. 카카오맵 api를 통한 주변 편의점 개수 확인](#카카오맵-api를-통한-주변-편의점-개수-확인)
  * [1-12. 사업장주소 주변 버스정류장 개수 찾기](#사업장주소-주변-버스정류장-개수-찾기)
  * [1-13. dart에서 업종코드 가져와서 섹터 정비](#dart에서-업종코드-가져와서-섹터-정비)
  * [1-14. 데이터 결합 및 변수 생성](#데이터-결합-및-변수-생성)
  * [1-15. 데이터 통합](#데이터-통합)
  * [1-16. 데이터 도산 여부 정의 및 sbhi 입력](#데이터-도산-여부-정의-및-sbhi-입력)
* [2. 데이터 전처리](#데이터-전처리)
  * [2-1. 결측치 처리 및 설립일자 이상치 제거](#결측치-처리-및-설립일자-이상치-제거)
  * [2-2. feature 보정 및 데이터 선정](#feature-보정-및-데이터-선정)
* [3. 모델링](#모델링)
  * [3-1. 재무 feature와 비재무 feature 결합 모델링](#재무-feature와-비재무-feature-결합-모델링)
    * [3-1-1. 상관관계 높은 개별 feature에 pca](#상관관계-높은-개별-feature에-pca)
    * [3-1-2. 로지스틱 모델링](#로지스틱-모델링)
    * [3-1-3. svm](#svm)
    * [3-1-4. 의사결정트리](#의사결정트리)
    * [3-1-5. knn](#knn)
    * [3-1-6. 앙상블_보팅](#앙상블_보팅)
    * [3-1-7. 앙상블_랜덤 포레스트](#앙상블_랜덤-포레스트)
    * [3-1-8. 앙상블_xgboost](#앙상블_xgboost)
    * [3-1-9. k_fold cross validation](#k_fold-cross-validation)
  * [3-2. 재무 feature 모델링](#재무-feature-모델링)
    * [3-2-1. 재무 feature만 가져오기](#재무-feature만-가져오기)
    * [3-2-2. 로지스틱 모델링_재무](#로지스틱-모델링_재무)
    * [3-2-3. svm_재무](#svm_재무)
    * [3-2-4. 의사결정트리_재무](#의사결정트리_재무)
    * [3-2-5. knn_재무](#knn_재무)
    * [3-2-6. 앙상블_보팅_재무](#앙상블_보팅_재무)
    * [3-2-7. 앙상블_랜덤 포레스트_재무](#앙상블_랜덤-포레스트_재무)
    * [3-2-8. 앙상블_xgboost_재무](#앙상블_xgboost_재무)
    * [3-2-9. k_fold cross validation_재무](#k_fold-cross-validation_재무)
* [4. 시각화](#시각화)
  * [4-1. 법정동코드 가져오기](#법정동코드-가져오기)
  * [4-2. 좌표계 위치데이터 시각화](#좌표계-위치데이터-시각화)
  * [4-3. 비재무적 지표 파이그래프 및 feature 보정 전후 비교](#비재무적-지표-파이그래프-및-feature-보정-전후-비교)
* [5. 테스트 데이터 전처리](#테스트-데이터-전처리)
  * [5-1. 섹터별 sbhi 가져오기](#섹터별-sbhi-가져오기)
  * [5-2. 테스트 데이터 수치변환 및 feature 선정](#테스트-데이터-수치변환-및-feature-선정)
  * [5-3. 테스트 데이터 표준화 및 개별 pca](#테스트-데이터-표준화-및-개별-pca)
* [6. 모델 테스트](#모델-테스트)
  * [6-1. 테스트 데이터 활용 모델 테스트](#테스트-데이터-활용-모델-테스트)
  * [6-2. 예측결과 비교](#예측결과-비교)
  
## 데이터 수집
#### 국민연금 사업장 데이터와 기업코드 병합
> 1_국민연금과 기업코드 병합.ipynb
1. [공공데이터포털(국민연금공단_국민연금 가입 사업장 내역)](https://www.data.go.kr/data/15083277/fileData.do) 데이터 다운 (2020년 1월 ~ 12월)
2. 1월 데이터 기준 _ 유한회사, SPAC 등 분석 목적과 관련 없는 기업 제거 / 중복 기업 제거
3. 1월 데이터 기준 _ ~12월 데이터 left join
4. [공공데이터포털(금융감독원_공시정보_고유번호)](https://www.data.go.kr/data/15060603/openapi.do) 데이터 다운
5. 국민연금 사업장 데이터와 공시대상 기업 코드 데이터를 **기업명 기준** inner join
~~~python
import numpy as np
import pandas as pd
Jan = pd.read_csv('파일이 저장되어 있는 경로', encoding = 'cp949')
Feb = pd.read_csv('파일이 저장되어 있는 경로', encoding = 'cp949')
Mar = pd.read_csv('파일이 저장되어 있는 경로', encoding = 'cp949')
Apr = pd.read_csv('파일이 저장되어 있는 경로', encoding = 'cp949')
May = pd.read_csv('파일이 저장되어 있는 경로', encoding = 'cp949')
Jun = pd.read_csv('파일이 저장되어 있는 경로', encoding = 'cp949')
Jul = pd.read_csv('파일이 저장되어 있는 경로', encoding = 'cp949')
Aug = pd.read_csv('파일이 저장되어 있는 경로', encoding = 'cp949')
Sep = pd.read_csv('파일이 저장되어 있는 경로', encoding = 'cp949')
Oct = pd.read_csv('파일이 저장되어 있는 경로', encoding = 'cp949')
Nov = pd.read_csv('파일이 저장되어 있는 경로', encoding = 'cp949')
Dec = pd.read_csv('파일이 저장되어 있는 경로', encoding = 'cp949')
One = pd.merge(Jan, Feb, on = ['사업장명', '사업장지번상세주소'], how = 'left')
merge_df_previous = Jan
for month in Months:
    merge_df = pd.merge(merge_df_previous, month, on = ['사업장명', '사업장지번상세주소', '사업장도로명상세주소'], how = 'left')
    merge_df_previous = merge_df
merge_df_previous = merge_df
merge_df = pd.merge(merge_df_previous, Dec, on = ['사업장명', '사업장지번상세주소', '사업장도로명상세주소'], how = 'left')
Corp_code = pd.read_csv('파일이 저장되어 있는 경로', encoding = 'cp949')
Corp_code_merge = pd.merge(merge_df, Corp_code, left_on = '사업장명', right_on = 'corp_name')
Corp_code_merge.to_csv('파일저장명')
~~~
#### 기업 개황 api를 이용하여 데이터 정제하기
>2_기업 개황 api를 통한 데이터 정제.ipynb
1. 1_1에서의 데이터 'corp_code'를 사용하여 [공공데이터포털(금융감독원_공시정보_기업개황)](https://www.data.go.kr/data/15034604/openapi.do) api를 통해 해당 기업의 사업장 주소와 대표자명, 설립일자 저장
2. 기존 1_1 데이터의 사업장 주소와 api의 사업장 주소를 비교 후 동일한 경우를 제외하고는 삭제
3. 대표자명과 설립일자를 column으로 추가
~~~python
import requests
import pandas as pd
url = '	https://opendart.fss.or.kr/api/company.json'
data_cln = []

for i in range(len(address_data)):
    
    try:
        print(i, '번째 진행중')

        code = codes[i]

        params = {
            'crtfc_key' : '748e6cf7dbae9f945e11c5d039fd70bafb0f5166',
            'corp_code' : str(code).rjust(8, '0')
        }

        res = requests.get(url, params = params)
        address_api = res.json()['adres']
        address_api_split = address_api.split()[0:2]

        address_data_split = address_data[i].split()[0:2]


        if address_api_split == address_data_split:

            _dict = dict(data.iloc[i])
            _dict['대표자명'] = res.json()['ceo_nm']
            _dict['설립일자'] = res.json()['est_dt']

            data_cln.append(_dict)
            
    except:
        
        print('error')
        
 data_cln = pd.DataFrame(data_cln)
 data_cln.to_csv('', encoding = 'cp949')
 ~~~
 #### 워크넷에서 재무제표와 사업자등록번호 가져오기
 > 3_워크넷에서 재무제표, 사업자등록번호 불러오기.ipynb
1. [워크넷](https://www.work.go.kr/seekWantedMain.do)에서 기업명과 사업장주소를 통해 동일한 기업에 대해 사업자등록번호와 재무제표를 가져옴
2. 검색결과가 없거나 검색은 되지만 재무제표가 없는 경우 비고란에 별도로 기재
> 결과 데이터 : 'corp_finstat_2020_(지역).csv' / ''corp_finstat_2021_(지역).csv'
~~~python
import requests
import pandas as pd
import time
from urllib import parse
from bs4 import BeautifulSoup

data = pd.read_csv('파일이 저장되어 있는 ', encoding = 'cp949')
data = data[['corp_name', '사업장도로명상세주소']]
cl = data['사업장도로명상세주소'].str.split().to_list()
### 오류나면 '++' 지우고 다시 시도
cl = pd.DataFrame(cl, columns = ['도, 광역시', '시, 군, 구', '읍, 면, 로', '+', '++'])
cl = cl[['도, 광역시', '시, 군, 구']]
cl = cl.replace('전라남도', '전남') # 지역에 맞게 수정 예시 (광주광역시 -> 광주)
data['address'] = cl['도, 광역시'] + ' ' + cl['시, 군, 구']
data.drop(['사업장도로명상세주소'], axis = 1, inplace = True)
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
options = webdriver.ChromeOptions()
import time
# 워크넷 로그인 
browser = webdriver.Chrome('개인 chromedriver 경로')
url="https://www.work.go.kr/member/bodyLogin.do?redirectUrl=/seekWantedMain.do"
browser.get(url)
id = browser.find_element(By.CSS_SELECTOR, '#custId1')
id.click()
time.sleep(1)
id.send_keys('개인ID')
password = browser.find_element(By.CSS_SELECTOR, '#pwd1')
password.click()
time.sleep(1)
password.send_keys('개인PW')
browser.find_element(By.CSS_SELECTOR, '#tab1 > div.put-info > div.login-area > button').click()
## 팝업창 없애는 코드, 오류나면 그냥 넘기기
browser.switch_to.window(browser.window_handles[1])
browser.close()
browser.switch_to.window(browser.window_handles[0])
list_corp_name = data['corp_name']
list_address = data['address']
corp_finstat_2020 = []
corp_finstat_2021 = []
for corp_name, address in zip(list_corp_name, list_address):
    
    # 재무제표 조회 초기값 설정 : 검색결과가 없을 때
    each_finstat_2020 = {}
    each_finstat_2020['corp_name'] = corp_name
    each_finstat_2020['비고'] = '검색결과 없음'
    
    
    each_finstat_2021 = {}
    each_finstat_2021['corp_name'] = corp_name
    each_finstat_2021['비고'] = '검색결과 없음'
    
    
    # 회사 이름으로 검색
    browser.switch_to.window(browser.window_handles[0])
    url = 'https://www.work.go.kr/wnSearch/unifSrch.do?colName=tb_bizinfo&query={}'.format(corp_name)
    browser.get(url)
    time.sleep(1)
    
    
    # 검색 페이지에 뜨는 회사 개수 파악 : 한 페이지만
    num = len(browser.find_elements(By.CSS_SELECTOR, 'div.result-company-list > ul > li'))
    
    
    # 검색 페이지에 회사(li)가 하나라도 뜨면 진행
    try:
        
        # 각 회사가 담긴 li에서 주소 가져오기
        for i in range(1, num + 1):
            each_path = f'div.result-company-list > ul > li:nth-child({i}) > div.cont > p:nth-of-type(2) > strong'
            searched_address = browser.find_element(By.CSS_SELECTOR, each_path).text

            # 찾은 주소와 가지고 있는 주소가 같으면 클릭
            if address in searched_address:
                searchbox_path = f'div.result-company-list > ul > li:nth-child({i}) > div.cont > a'
                searchbox = browser.find_element(By.CSS_SELECTOR, searchbox_path)
                searchbox.click()
                
                # 사업자등록번호 가져오기
                html = browser.page_source
                soup = BeautifulSoup(html, 'html.parser')
                
                business_number = soup.select(searchbox_path)[0]['onclick']
                business_number = business_number.split("'")[3]
                
                
                
                # 재무제표가 존재하는 경우 try
                try:
                    browser.switch_to.window(browser.window_handles[1])
                    
                    # 팝업된 페이지에서 재무제표 더보기 클릭
                    finstat_more_path = '#companySection04 > div:nth-child(4) > div.default > div.btn.mt10.a-r > button'
                    finstat_more =  WebDriverWait(browser, 3).until(EC.presence_of_element_located((By.CSS_SELECTOR, finstat_more_path)))
                    finstat_more.click()
                    
                    # 팝업된 페이지에서 재무비율 더보기 클릭
                    finrate_more_path = '#companySection04 > div:nth-child(6) > div.default > div.relative > div > button'
                    finrate_more = WebDriverWait(browser, 3).until(EC.presence_of_element_located((By.CSS_SELECTOR, finrate_more_path)))
                    finrate_more.click()

                    
                    # BeautifulSoup을 이용하여 팝업된 페이지 가져오기
                    html = browser.page_source
                    soup = BeautifulSoup(html, 'html.parser')
                    
                    # 팝업 브라우저 닫기
                    browser.close()

                    # 재무제표 테이블 가져오기
                    fin_path = '#companySection04 > div.table-show-hide.on > div.no-default > div.careers-table.center.small.v2 > table'
                    finstat_table = soup.select(fin_path)[0]
                    
                    # 재무비율 테이블 가져오기
                    finrate_table = soup.select(fin_path)[1]


                    
                    # 각 해 재무제표를 each_year_dict 딕셔너리로 불러오고, 그것을 finstat 리스트에 저장하기
                    finstat = []

                    for i in range(3):
                        each_year_dict = {}

                        each_year_dict['계정명'] = finstat_table.select('thead > tr > th')[i + 2].text.strip()

                        
                        # 재무제표 테이블에서 key와 value 뽑기
                        for j in range(1, len(finstat_table.select('tbody > tr')) + 1):
                            key = finstat_table.select(f'tbody > tr:nth-of-type({j}) > td:nth-of-type(1)')[0].text.strip()
                            value = finstat_table.select(f'tbody > tr:nth-of-type({j}) > td:nth-of-type({i + 2})')[0].text.strip()

                            each_year_dict[key] = value

                            
                        # 재무비율 테이블에서 key와 value 뽑기
                        for j in range(1, len(finrate_table.select('tbody > tr')) + 1):
                            key = finrate_table.select(f'tbody > tr:nth-of-type({j}) > td:nth-of-type(1)')[0].text.strip()
                            value = finrate_table.select(f'tbody > tr:nth-of-type({j}) > td:nth-of-type({i + 2})')[0].text.strip()

                            each_year_dict[key] = value
                        
                        finstat.append(each_year_dict)

                        
                    # finstat 리스트를 데이터프레임으로 저장하고, 인덱스를 연도(계정명)으로 지정하기
                    finstat_df = pd.DataFrame(finstat).set_index('계정명')


                    
                    # 2020, 2021년 재무제표 & 재무비율만 가져와 each_finstat_2020, each_finstat_2021에 저장하기
                    
                    if '2020-12-31' in finstat_df.index:
                        each_finstat_2020 = dict(finstat_df.loc['2020-12-31'])
                        each_finstat_2020['corp_name'] = corp_name
                        each_finstat_2020['사업자등록번호'] = business_number
                    
                    # 2020년만 없을 경우
                    else:
                        each_finstat_2020['사업자등록번호'] = business_number
                        each_finstat_2020['비고'] = '재무제표 없음'
                        
                        
                    
                    if '2021-12-31' in finstat_df.index:
                        each_finstat_2021 = dict(finstat_df.loc['2021-12-31'])
                        each_finstat_2021['corp_name'] = corp_name
                        each_finstat_2021['사업자등록번호'] = business_number
                        
                    
                    # 2021년만 없을 경우
                    else:
                        each_finstat_2021['사업자등록번호'] = business_number
                        each_finstat_2021['비고'] = '재무제표 없음'

                            
                        
                            
                            
                # 재무제표가 아예 존재하지 않는 경우
                except:
                    each_finstat_2020['사업자등록번호'] = business_number
                    each_finstat_2020['비고'] = '재무제표 없음'
                    
                    
                    each_finstat_2021['사업자등록번호'] = business_number
                    each_finstat_2021['비고'] = '재무제표 없음'
                    
                    

                # 한 개 회사에서 재무제표 가져왔으므로, 주소를 비교하는 반복문 break
                break
        
        
        # 최종적으로 재무제표 조회 결과를 corp_finstat_2020에 추가
        corp_finstat_2020.append(each_finstat_2020)
        corp_finstat_2021.append(each_finstat_2021)
                
    except:
        corp_finstat_2020.append(each_finstat_2020)
        corp_finstat_2021.append(each_finstat_2021)
# 인덱스를 기업명으로 하여 2020년 재무제표 데이터프레임 생성

corp_finstat_2020_(지역)_df = pd.DataFrame(corp_finstat_2020).set_index('corp_name')
corp_finstat_2020_(지역)_df.to_csv('corp_finstat_2020_(지역).csv', encoding = 'cp949')

# 인덱스를 기업명으로 하여 2021년 재무제표 데이터프레임 생성

corp_finstat_2021_(지역)_df = pd.DataFrame(corp_finstat_2021).set_index('corp_name')
corp_finstat_2021_(지역)_df.to_csv('corp_finstat_2021_(지역).csv', encoding = 'cp949')
~~~
#### dart에서 사업자등록번호 가져오기
> 4_dart에서 사업자등록번호 가져오기.ipynb
1. 폐업된 기업들은 [워크넷](https://www.work.go.kr/seekWantedMain.do)에서 검색되지 않으므로, [dart](https://dart.fss.or.kr/main.do)에서 추가적으로 사업자등록번호를 가져오기
> 결과 데이터 : 'corp_finstat_2020_(지역)_2.csv'
~~~python
import pandas as pd
## 기존 워크넷 재무제표 크롤링 결과 가져오기

corp_finstat = pd.read_csv('corp_finstat_2020_(지역).csv 저장되어 있는 경로', encoding = 'cp949')
corp_nps = pd.read_csv('지역별 기업코드와 국민연금 사업장/(지역).csv 저장되어 있는 경로', encoding = 'cp949')

## corp_nps에 비고란 추가
corp_nps['비고'] = corp_finstat['비고']
## 비고란이 '검색결과 없음'인 기업들만 추려서 가져옴
noresult_corp_nps = corp_nps.loc[corp_nps['비고'] == '검색결과 없음']
list_corp_name = noresult_corp_nps['corp_name']
list_ceo_name = noresult_corp_nps['대표자명']
list_index = list_corp_name.index

from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.support import expected_conditions as EC
options = webdriver.ChromeOptions()

from bs4 import BeautifulSoup
import re
import time

browser = webdriver.Chrome('개인 chromedriver 경로')
list_business_number = []

for index, corp_name, ceo_name in zip(list_index, list_corp_name, list_ceo_name):
    
    print(index + 1, '행 진행중')
    url = "https://dart.fss.or.kr/dsab007/main.do?option=corp"
    browser.get(url)
    
    
    ## 기업 검색 ##

    # 기업명 입력
    input_corp_name = browser.find_element(By.CSS_SELECTOR, '#textCrpNm')
    input_corp_name.send_keys(corp_name)
    
    # 위 검색명 옆 돋보기 클릭
    SearchCorp_path = '#btnCorp'
    browser.find_element(By.CSS_SELECTOR, SearchCorp_path).click()
    
    
    time.sleep(0.5)
    
    # 검색된 기업의 개수 (하나도 없으면 num = 1)
    num = len(browser.find_elements(By.CSS_SELECTOR, '#corpListContents > div.tbLWrap > div.tbLInner > table > tbody > tr'))

    
    # 검색된 각 기업마다 ~
    for i in range(num):

        # 각 기업의 대표자명 추출
        searched_ceo_name = browser.find_elements(By.CSS_SELECTOR, '#corpListContents > div.tbLWrap > div.tbLInner > table > tbody > tr > td:nth-of-type(3)')[i].text

        # 추출된 대표자명과 갖고 있는 데이터의 대표자명이 같으면, 사업자등록번호 가져오기
        if ceo_name == searched_ceo_name:
            CorpTitle_path = f'#corpListContents > div.tbLWrap > div.tbLInner > table > tbody > tr:nth-child({i + 1}) > td:nth-child(1)'
            
            html = browser.page_source
            soup = BeautifulSoup(html, 'html.parser')
            
            title = soup.select(CorpTitle_path)[0]['title']
            business_number = re.findall('\d+\-\d+\-\d+', title)[0]
            business_number = business_number.replace('-', '')
            
            
            each_dict_business_number = {}
            each_dict_business_number['index'] = index
            each_dict_business_number['corp_name'] = corp_name
            each_dict_business_number['사업자등록번호'] = business_number
            
            list_business_number.append(each_dict_business_number)
            
            break

# 인덱스에 맞춰서 사업자등록번호 채워넣기
df_business_number = pd.DataFrame(list_business_number).set_index('index')
corp_finstat.loc[list_index, '사업자등록번호'] = df_business_number['사업자등록번호']
corp_finstat.to_csv('corp_finstat_2020_(지역)_2.csv', encoding = 'cp949', index = False)
~~~

#### 사업자등록번호를 통해 폐업 여부 조회하기
> 5_사업자등록번호로 국세청에서 폐업여부 확인하기.ipynb
1. 'corp_finstat_2020_(지역)_2.csv'의 사업자등록번호를 추출
2. [국세청홈택스](https://hometax.go.kr/websquare/websquare.html?w2xPath=/ui/pp/index.xml) 에 사업자등록번호를 검색
3. 계속사업자의 경우 정상, 폐업자의 경우 폐업을 기재
4. 폐업자의 경우 폐업일자도 추가로 기재
> 결과 데이터 : 'corp_finstat_2020_(지역)_3.csv'
~~~python
import pandas as pd
import numpy as np
# dart에서 사업자등록번호 가져온 csv 파일
data = pd.read_csv('corp_finstat_2020_(지역)_2.csv가 저장되어 있는 경로', encoding = 'cp949')
data_notnull = data.loc[data['사업자등록번호'].notnull()]
list_business_number = data_notnull['사업자등록번호']
list_index = list_business_number.index

from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.common.keys import Keys
from selenium.webdriver import ActionChains
from selenium.webdriver.support import expected_conditions as EC
options = webdriver.ChromeOptions()

from bs4 import BeautifulSoup
import re
import time

browser = webdriver.Chrome('개인 chromedriver 경로')
url = 'https://hometax.go.kr/websquare/websquare.html?w2xPath=/ui/pp/index.xml'
browser.get(url)
# 조회/발급 버튼 클릭
Search_button = browser.find_element(By.CSS_SELECTOR, '#group1300')
Search_button.click()
# 내부 프레임으로 전환
browser.switch_to.frame('txppIframe')
# 사업자등록번호로 조회 클릭
Bisno_Search_button = browser.find_element(By.CSS_SELECTOR, '#sub_a_0108010000')
Bisno_Search_button.click()
status = []

for index, business_number in zip(list_index, list_business_number):
    print(index + 1, '행 진행중')
    
    # 사업자등록번호 입력

    browser.find_element(By.CSS_SELECTOR, '#bsno').click()
    browser.find_element(By.CSS_SELECTOR, '#bsno').send_keys(int(business_number))
    
    # 조회버튼 클릭
    browser.find_element(By.CSS_SELECTOR, '#trigger5').click()
    
    time.sleep(1)
    
    # 조회결과 가져오기
    text = browser.find_element(By.CSS_SELECTOR, '#grid2_cell_0_1 > span').text
    
    
    # 각 사업자등록번호별 상태 딕셔너리
    each_status = {}
    each_status['index'] = index
    
    if '폐업자' in text:
        each_status['사업자 상태'] = '폐업'
        each_status['폐업일자'] = re.findall('\d+\-\d+\-\d+', text)[0]
        
    else:
        each_status['사업자 상태'] = '정상'
        
    
    status.append(each_status)
    
df_status = pd.DataFrame(status).set_index('index')
data['사업자 상태'] = df_status['사업자 상태']
data['폐업일자'] = df_status['폐업일자']
data.to_csv('corp_finstat_2020_(지역)_3.csv', encoding = 'cp949', index = False)
~~~
#### 필요한 변수만 남기기
> 6_1_corp_finstat_2020_3 파일에서 필요한 변수만 남기기.ipynb
1. 재무제표가 담긴 'corp_finstat_2020_(지역)_3.csv' 파일에서 필요한 변수만 남김
~~~python
import pandas as pd
region="지역" # 해당 지역으로 수정하기
data = pd.read_csv(f'corp_finstat_2021_{region}_3.csv가 저장되어 있는 경로', encoding = 'cp949',thousands = ',')
data['매출총이익']=data['매출총이익'].str.replace(",","")
data['매출액']=data['매출액'].str.replace(",","")
sale_total_profit_rate=[]

for i in range(len(data)):
    rate={}
    try:
        rate["매출총이익률"]=round(float(data["매출총이익"][i])/float(data["매출액"][i])*100,1)
        sale_total_profit_rate.append(rate)
    except:
        rate["매출총이익률"]=""
        sale_total_profit_rate.append(rate)

sale_total_profit_rate_df=pd.DataFrame(sale_total_profit_rate)
data["매출총이익률"]=sale_total_profit_rate_df["매출총이익률"]
# column 네이밍
data=data[["corp_name","비고","순이익률","영업이익률","매출총이익률","총자산순이익률(ROA)","자본금이익률(ROE)","매출액증가율","영업이익증가율","순이익증가율","총자본회전율","자기자본회전율","부채비율","유동성비율","당좌비율","자기자본비율","사업자등록번호","사업자 상태","폐업일자"]]
data.to_csv(f'selected_feature({region}).csv',encoding="cp949",index=False)
~~~

#### 캐치에서 기업형태 및 산업군 가져오기
> 7_1_캐치에서 기업규모와 섹터 가져오기.ipynb
1. [캐치](https://www.catch.co.kr/)에 접속하여 로그인
2. 기업이름 검색을 통해 기업의 기업형태, 산업군 가져오기
> 결과 데이터 : 'corp_nps_(지역)_2.csv'

~~~python
import pandas as pd
import numpy as np
corp_nps = pd.read_csv('파일이 저장되어 있는 경로', encoding = 'cp949')
data = corp_nps[['corp_name', '대표자명', '사업장도로명상세주소']]
cl = data['사업장도로명상세주소'].str.split().to_list()
### 오류나면 '++' 지우고 다시 시도
cl = pd.DataFrame(cl, columns = ['도, 광역시', '시, 군, 구', '읍, 면, 로', '+', '++'])
cl = cl[['도, 광역시', '시, 군, 구']]
cl = cl.replace('전라남도', '전남') # 지역에 맞게 수정 예시 (광주광역시 -> 광주)
data['address'] = cl['도, 광역시'] + ' ' + cl['시, 군, 구']
list_corp_name = data['corp_name']
list_ceo_name = data['대표자명'].str.replace(' ', '')
list_address = data['address']

from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.support import expected_conditions as EC
options = webdriver.ChromeOptions()

from bs4 import BeautifulSoup
import time

browser = webdriver.Chrome('개인 chromedriver 경로')
browser.set_window_size(2048, 1024)
browser.get('https://www.catch.co.kr/')
browser.find_element(By.CSS_SELECTOR, '#header_wrap > div.main_header > div.main_header_group1 > div.btns > a.login').click()
# 아이디 입력
browser.find_element(By.CSS_SELECTOR, '#id_login').send_keys('개인ID')
# 비밀번호 입력
browser.find_element(By.CSS_SELECTOR, '#pw_login').send_keys('개인PW')
# 로그인 버튼 클릭
browser.find_element(By.CSS_SELECTOR, '#wrapper > div > div.mem_contents > div > p.mem_btn_full > a').click()
list_corp_name = data['corp_name']
list_ceo_name = data['대표자명'].str.replace(' ', '')
list_address = data['address']
list_sector_scale = []
# 크롤링 대상 사이트 접속
url = 'https://www.catch.co.kr/Comp/CompMajor'
browser.get(url)
# 취업특강 배너 없애기
browser.find_element(By.CSS_SELECTOR, '#layerStepInfo > button').click()
# 크롤링 대상 지역이 전남, 경북, 경남, 제주라면 '지역별' 영역 스크롤 내리기
if 지역 in ['전남', '경북', '경남', '제주']:
    category_region = WebDriverWait(browser, 3).until(EC.presence_of_element_located((By.CSS_SELECTOR, '#Contents > div.corp_src > div.top.at4 > dl:nth-child(2) > dd')))
    browser.execute_script("arguments[0].scrollBy(0, 50)", category_region)


# 크롤링 대상 지역 클릭
region = f'#chkSido{지역}'
browser.find_element(By.CSS_SELECTOR, region).click()

for corp_name, ceo_name, address in zip(list_corp_name, list_ceo_name, list_address):
    
    # 한 개 기업에 대한 크롤링 정보 담을 딕셔너리 생성
    each_sector_scale = {}
    each_sector_scale['corp_name'] = corp_name
    
    
    ## 메인 기업분석 화면에서 지역을 고르고 기업 이름 검색 ##
    
    
    # 대표자명의 형식이 일정하지 않으므로, 공백을 제거한 뒤 최대 3자리를 비교하고자 한다
    ceo_name_tr = ceo_name[0 : np.min([len(ceo_name), 3])]
    

    # 기업 이름 입력
    browser.find_element(By.CSS_SELECTOR, '#CompName').click()
    browser.find_element(By.CSS_SELECTOR, '#CompName').send_keys(corp_name)
    
    
    # 검색 버튼 클릭
    browser.find_element(By.CSS_SELECTOR, '#imgSearch').click()
    
    time.sleep(3)
    
    
    
    ## 기업 검색 후 ##
    
    # 검색된 기업의 개수
    num = len(browser.find_elements(By.CSS_SELECTOR, '#updates > tbody > tr > td > dl'))
    
    
    # 검색된 각 기업마다 url 가져오기
    list_corp_url = []
    try:                                                                
        for i in range(num):                                                
            # 그냥 링크를 클릭하면 백그라운드 상태에서는 페이지가 넘어가지 않아서, url을 가져온다
            html = browser.page_source
            soup = BeautifulSoup(html, 'html.parser')
            link = soup.select(f'#updates > tbody > tr > td > dl > dt:nth-child(2) > a')[i]['href']
            corp_url = 'https://www.catch.co.kr' + link

            list_corp_url.append(corp_url)

    except:
        list_sector_scale.append(each_sector_scale)
        continue

     # 검색된 각 기업마다 ~
    for i in range(num):
        # 각 기업의 상세기업정보로 이동
        browser.execute_script(f'window.open("{list_corp_url[i]}");')
        browser.switch_to.window(browser.window_handles[1])
        
        
        ## 상세기업정보 화면에서 ##
        
        # 대표자명과 주소 중 하나만 일치하면 갖고 있는 데이터와 동일 기업으로 간주
        # 대표자명은 dart 기준이므로, 반영이 느린 경우가 많다
        # 검색대상 기업이 사업장을 옮긴 경우가 있어서, 주소가 다른 경우도 있다
        
        
        # 찾은 대표자명
        searched_ceo_name_path = '#Contents > div:nth-child(2) > div:nth-child(1) > div.corp_detail_box > table > tbody > tr:nth-child(1) > td:nth-child(2)'
        searched_ceo_name = browser.find_element(By.CSS_SELECTOR, searched_ceo_name_path).text

        # 찾은 사업장주소
        searched_address_path = '#Contents > div:nth-child(2) > div.corp_detail_box > div.top > p'
        searched_address = browser.find_element(By.CSS_SELECTOR, searched_address_path).text
        

        
        # 동일 기업이라면 ~  (주소의 경우 앞에서 두개가 일치하면)
        if (searched_ceo_name == ceo_name_tr) or searched_address.split()[0:2] == address.split()[0:2]:
            
            # 섹터 크롤링
            sector_path = '#Contents > div:nth-child(1) > div.corp_detail_top > div.inner > div.name > p > span'
            sector = browser.find_element(By.CSS_SELECTOR, '#Contents > div:nth-child(1) > div.corp_detail_top > div.inner > div.name > p > span').text
            
            # 기업규모 크롤링
            business_scale_path = '#Contents > div:nth-child(2) > div:nth-child(1) > div.corp_detail_box > table > tbody > tr:nth-child(2) > td:nth-child(2)'
            business_scale = browser.find_element(By.CSS_SELECTOR, '#Contents > div:nth-child(2) > div:nth-child(1) > div.corp_detail_box > table > tbody > tr:nth-child(2) > td:nth-child(2)').text
            
            
            # 딕셔너리에 섹터와 기업규모 정보 담기
            each_sector_scale['sector'] = sector
            each_sector_scale['business_scale'] = business_scale
            
            
            # 해당 기업에 대한 크롤링이 끝났으므로, break
            browser.close()
            browser.switch_to.window(browser.window_handles[0])
            break
        
        
        # 동일 기업이 아니라면 창 닫고 다음 기업 링크로 가기
        else:
            browser.close()
            browser.switch_to.window(browser.window_handles[0])
            
    list_sector_scale.append(each_sector_scale)
    
df_sector_scale = pd.DataFrame(list_sector_scale)

corp_nps['섹터'] = df_sector_scale['sector']
corp_nps['기업규모'] = df_sector_scale['business_scale']

corp_nps.to_csv('corp_nps_(지역)_2.csv', encoding = 'cp949')

~~~

#### 잡플래닛에서 기업형태 및 산업군 가져오기
> 7_2_잡플래닛에서 기업규모와 섹터 져오기.ipynb
1. [캐치](https://www.catch.co.kr/)에서 검색되지 않은 기업들에 대해 [잡플래닛](https://www.jobplanet.co.kr/welcome/index)에서 보완
2. 주소비교를 통해 동일한 기업에 대해 형태 및 산업군 가져오기 
> 결과물 : 'corp_nps_(지역)_3.csv'
~~~python 
import requests
import pandas as pd
import time

from urllib import parse
from bs4 import BeautifulSoup

from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
options = webdriver.ChromeOptions()

data = pd.read_csv('corp_nps_(지역)_2.csv가 저장되어 있는 경로', encoding = 'cp949')

# data 정제 
data = data[['corp_name', '사업장도로명상세주소_x', '섹터', '기업규모']]
cl = data['사업장도로명상세주소_x'].str.split().to_list()
cl = pd.DataFrame(cl, columns = ['도, 광역시', '시, 군, 구', '읍, 면, 로', '+', '++'])
cl = cl[['도, 광역시', '시, 군, 구']]
# 자신에게 맞는 지역으로 바꿔주기
cl = cl.replace('경기도', '경기')
data['address'] = cl['도, 광역시'] + ' ' + cl['시, 군, 구']
data.drop(['사업장도로명상세주소_x'], axis = 1, inplace = True)

browser = webdriver.Chrome('개인 chromedriver 경로')

for i in range(len(data)):
#for i in range(10):
    # '섹터' 또는 '기업규모' 피처가 NaN 값이면
    try:
        if (pd.isnull(data.iloc[i]['섹터']) or pd.isnull(data.iloc[i]['기업규모'])):
            url = 'https://www.jobplanet.co.kr/search?query={}'.format(data.iloc[i]['corp_name'])
            browser.get(url)
            time.sleep(0.5)
            #browser.find_element(By.CSS_SELECTOR, 
                                #'#jpfollow_induce_panel > button').click()
            # 검색된 회사 갯수
            num = len(browser.find_elements(By.CSS_SELECTOR, 'div.is_company_card > div'))
            if num == 0:
                continue
            # 검색된 회사가 있다면
            for k in range(1, num+1):
                if k > 1:
                # 하나 보고난 다음에는 다시 초기화면으로 전환
                    url = 'https://www.jobplanet.co.kr/search?query={}'.format(data.iloc[i]['corp_name'])
                    browser.get(url)
                searchbox_path = f'#mainContents > div:nth-child(1) > div > div.result_company_card > div.is_company_card > div:nth-child({k}) > a'
                searchbox = browser.find_element(By.CSS_SELECTOR, searchbox_path)
                searchbox.click()
                time.sleep(3)
                # '뉴스룸' 카테고리에서 주소 비교'
                newsroom_path = '#viewCompaniesMenu > ul > li.viewCompanies > a'
                newsroom = browser.find_element(By.CSS_SELECTOR, newsroom_path)
                newsroom.click()
                time.sleep(1)
                addr_path = '#contents_wrap > div > div:nth-child(1) > div > div > div.basic_info_sec > div > ul.basic_info_more > li:nth-child(3) > dl > dd'
                searched_address = browser.find_element(By.CSS_SELECTOR, addr_path).text
                # 주소가 '시'까지 똑같으면 동일 회사로 취급 '
                if data.iloc[i]['address'] == ' '.join(searched_address.split(' ')[:2]):
                    # 산업 및 기업 형태 가져오기
                    sector_path = '#contents_wrap > div > div:nth-child(1) > div > div > div.basic_info_sec > div > ul.basic_info_list > li:nth-child(1) > div > div > strong'
                    sector = browser.find_element(By.CSS_SELECTOR, sector_path).text
                    data.iloc[i]['섹터'] = sector
                    type_path = '#contents_wrap > div > div:nth-child(1) > div > div > div.basic_info_sec > div > ul.basic_info_list > li:nth-child(2) > div > div > strong'
                    corp_type = browser.find_element(By.CSS_SELECTOR, type_path).text
                    data.iloc[i]['기업규모'] = corp_type
                    break
        else:
            continue
    except: # 갑자기 팝업뜨면 멈출 수 있음
        # 팝업 창 제거 
        browser.find_element(By.CSS_SELECTOR, '#premiumReviewChart > div > div.layer_popup_box.layer_popup_box_on > div.layer_popup.jply_modal.premium_review_inform > div > div.premium_modal_header > button').click()
        print('index = ',i,'/ corp_name = ',data.iloc[i]['corp_name'],'에서 팝업이 떴습니다')
        
result_data = pd.read_csv('corp_nps_(지역)_2.csv 저장되어 있는 경로', encoding = 'cp949')
result_data['섹터'] = data['섹터']
result_data['기업규모'] = data['기업규모']
result_data.to_csv('corp_nps_(지역)_3.csv', encoding = 'cp949')
~~~

#### dart에서 상세주소 가져오기
> 8_0_다트에서 상세주소 가져오기.ipynb
1. [dart](https://dart.fss.or.kr/main.do)의 api를 통해 상세주소를 가져옴
> 결과 데이터 : 'corp_nps_(지역)_4.csv'
~~~python
import requests
import pandas as pd
data=pd.read_csv('corp_nps_(지역)_3.csv가 저장되어 있는 경로',encoding='cp949')
list_code = data['corp_code']
list_corp_name = data['corp_name']
url = 'https://opendart.fss.or.kr/api/company.json'

detail_address = []

for corp_name, code in zip(list_corp_name, list_code):

    params = {
        'crtfc_key' : '개인인증키',
        'corp_code' : str(code).rjust(8, '0')
    }

    res = requests.get(url, params = params)
    
    print(corp_name, res.ok)
    
    _dict = {}
    
    _dict['corp_name'] = corp_name
    _dict['상세주소'] = res.json()['adres']

    detail_address.append(_dict)

df_detail_address = pd.DataFrame(detail_address)
data["상세주소"]=df_detail_address["상세주소"]
data.to_csv(f"corp_nps_{지역}_4.csv",encoding="cp949",index = False)
~~~
#### 카카오맵 api를 통한 위도 및 경도 찾기
> 8_1_각 위치별 경도 위도 찾기.ipynb
1. [카카오맵 api](https://apis.map.kakao.com/)에서 제공하는 api 기능을 통해 기업 주소의 위,경도 찾기
> 결과 데이터 : '위도경도확인_(지역).csv'
~~~python
import requests
import pandas as pd
import numpy as np
import json

data=pd.read_csv("corp_nps_(지역)_6.csv",encoding='cp949')
corp_name_list=data['corp_name']
add_list=data['상세주소']

final_list=[]

for corp_name, address in zip(corp_name_list,add_list):
    location_list={}
    location_list['corp_name'] = corp_name
    address_split=address.split()
    for i in range(len(address_split)):
        try:
            if len(address.split())<=3:
                location_list['위도'] = '조회 안됨'
                location_list['경도'] = '조회 안됨'
                final_list.append(location_list)
                break
            else:
                address_split=address.split()
                url='https://dapi.kakao.com/v2/local/search/address.json?query='+address
                headers={'Authorization':'KakaoAK 7b3683e0b4142b33db211d5ad72fab0a'} 
                result=json.loads(str(requests.get(url,headers=headers).text))
                longitude=result['documents'][0]['address']['x']
                latitude=result['documents'][0]['address']['y']
                location_list['위도'] = latitude
                location_list['경도'] = longitude
                final_list.append(location_list)
                break
        except:
            address_split=address.split()
            address = ' '.join(address_split[0 : len(address_split) - (i + 1)])
            
 location=pd.DataFrame(final_list)
 location.to_csv("위도경도확인_(지역).csv",encoding="cp949",index=False)
 ~~~
 
#### 카카오맵 api를 통한 주변 편의점 개수 확인
> 8_3_카카오맵 api를 통한 편의점 개수 확인.ipynb
1. [카카오맵 api](https://apis.map.kakao.com/)에서 제공하는 api 기능을 통해 주변 편의점 개수 조회
> 결과 데이터 : 'corp_nps_(지역)_6.csv'
~~~python
import requests
import pandas as pd
import numpy as np
import json

data=pd.read_csv("corp_nps_(지역)_4.csv가 저장되어 있는 경로",encoding='cp949')
corp_name_list=data['corp_name']
add_list=data['상세주소']

final_list=[]

for corp_name, address in zip(corp_name_list,add_list):
    conv_list={}
    conv_list['corp_name'] = corp_name
    address_split=address.split()
    for i in range(len(address_split)):
        try:
            if len(address.split())<=3:
                conv_list['주변 편의점 개수'] = '조회 안됨'
                final_list.append(conv_list)
                break
            else:
                print(address)
                address_split=address.split()
                url='https://dapi.kakao.com/v2/local/search/address.json?query='+address
                headers={'Authorization':'KakaoAK 7b3683e0b4142b33db211d5ad72fab0a'}
                result=json.loads(str(requests.get(url,headers=headers).text))
                longitude=result['documents'][0]['address']['x']
                latitude=result['documents'][0]['address']['y']
                
                url1 = 'https://dapi.kakao.com/v2/local/search/keyword.json'
                params={'query':'편의점','x':longitude,'y':latitude,'radius':500,'category_group_code':'CS2'}
                conv_num = requests.get(url1, params=params, headers=headers).json()['meta']['total_count']
                
                conv_list['주변 편의점 개수'] = conv_num            
                final_list.append(conv_list)
                break
        except:
            address_split=address.split()
            address = ' '.join(address_split[0 : len(address_split) - (i + 1)])
 num_of_conv=pd.DataFrame(final_list)
 data["주변 편의점 개수"]=num_of_conv['주변 편의점 개수']
 data.to_csv("corp_nps_(지역)_6.csv",encoding="cp949",index=False)
~~~
 
 #### 사업장주소 주변 버스정류장 개수 찾기
 > 8_4_사업장 주변 버스정류장 개수 가져오기.ipynb
 1. [공공데이터포털(국토교통부_전국 버스정류장 위치정보)](https://www.data.go.kr/data/15067528/fileData.do) 데이터 다운
 2. 이전 'corp_nps_(지역)_6.csv'와 '위도경도확인_(지역).csv' 파일을 활용하여 사업장 주변 500m 이내 버스정류장 개수 조회
 > 결과 데이터 : 'corp_nps_(지역)_7.csv'
 ~~~python
 # haversine 라이브러리 설치
 !pip install haversine
 
 import haversine as hs
from haversine import Unit
import pandas as pd

station_data = pd.read_csv('전국버스정류장 위치정보.csv가 저장되어 있는 경로', encoding = 'cp949')
list_station_latitude = station_data['위도']
list_station_longitude = station_data['경도']
list_index = list_station_latitude.index

corp_nps = pd.read_csv('corp_nps_{지역}_6.csv가 저장되어 있는 경로', encoding = 'cp949')
corp_data = pd.read_csv('위도경도확인_{지역}.csv'가 저장되어 있는 경로, encoding = 'cp949')

list_corp_code = corp_nps['corp_code']
list_corp_name = corp_data['corp_name']
list_corp_latitude = corp_data['위도']
list_corp_longitude = corp_data['경도']

list_nearby_station = []

for corp_name, corp_code, corp_latitude, corp_longitude in zip(list_corp_name, list_corp_code, list_corp_latitude, list_corp_longitude):
    
    num_of_nearby_station = None
    
    if corp_latitude != '조회 안됨':
        
        num_of_nearby_station = 0
        
        for index, station_latitude, station_longitude in zip(list_index, list_station_latitude, list_station_longitude):

            station_location = (station_latitude, station_longitude)
            corp_location = (float(corp_latitude), float(corp_longitude))


            distance = hs.haversine(corp_location, station_location, unit = Unit.METERS)

            if distance <= 500:
                num_of_nearby_station += 1
            
    
    each_nearby_station = {
        'corp_code' : corp_code,
        'corp_name' : corp_name,
        '정류장 개수' : num_of_nearby_station
    }
    
    
    list_nearby_station.append(each_nearby_station)
    
df_nearby_station = pd.DataFrame(list_nearby_station)

corp_nps['정류장 개수'] = df_nearby_station['정류장 개수']
## 폐기된 버스 노선 개수 drop
corp_nps.drop(['버스 노선 개수'], axis = 1, inplace = True)
corp_nps.to_csv(f'corp_nps_{지역}_7.csv', encoding = 'cp949', index = False)
~~~

#### dart에서 업종코드 가져와서 섹터 정비
> 8_5_다트 업종코드로 섹터 가져오기.ipynb
1. 기존 [캐치](https://www.catch.co.kr/)와 [잡플래닛](https://www.jobplanet.co.kr/welcome/index)에서 수집한 기업 섹터를 개선하기 위해 [opendart](https://opendart.fss.or.kr/)의 api를 통해 업종코드를 가져옴
2. 가져온 업종코드는 [공공데이터포털(고용노동부_업종코드)](https://www.data.go.kr/data/15049592/fileData.do)와 결합하여 21개의 섹터 중 하나로 배치(기존 섹터 column을 대체)
> 결과 데이터 : 'corp_nps_(지역)_8.csv'
~~~python
import requests
import pandas as pd

KSIC = pd.read_csv('고용노동부_업종코드_20220801.csv'가 저장되어 있는 경로, encoding = 'cp949')
# 업종코드와, 대분류, 중분류 가져오기
KSIC = KSIC[['대분류', '중분류', '업종코드']]
list_ksic_induty_code = KSIC['업종코드']
list_ksic_main_class = KSIC['대분류']
list_ksic_middle_class = KSIC['중분류']

# 업종코드를 넣으면 대분류를 출력해주는 딕셔너리

code_to_main_class = {}

for ksic_induty_code, ksic_main_class in zip(list_ksic_induty_code, list_ksic_main_class):
    code_to_main_class[ksic_induty_code] = ksic_main_class
    
# 중분류를 넣으면 대분류를 출력해주는 딕셔너리

middle_class_to_main_class = {}

for ksic_middle_class, ksic_main_class in zip(list_ksic_middle_class, list_ksic_main_class):
    middle_class_to_main_class[ksic_middle_class] = ksic_main_class

# 업종코드를 넣으면 중분류를 출력해주는 딕셔너리 : for 제조업 분류

code_to_middle_class = {}

for ksic_induty_code, ksic_middle_class in zip(list_ksic_induty_code, list_ksic_middle_class):
    code_to_middle_class[ksic_induty_code] = ksic_middle_class
    
# 기존 corp_nps 데이터

corp_nps = pd.read_csv("corp_nps_{지역}_7.csv가 저장되어있는 경로", encoding='cp949')

# corp_nps 데이터에서 기존 섹터 column 삭제

corp_nps.drop('섹터', axis = 1, inplace = True)
list_corp_code = corp_nps['corp_code']
list_corp_name = corp_nps['corp_name']

url = '	https://opendart.fss.or.kr/api/company.json'

corp_induty_class = []


# 각 기업마다 ~
for corp_name, corp_code in zip(list_corp_name, list_corp_code):
    params = {
        'crtfc_key' : '748e6cf7dbae9f945e11c5d039fd70bafb0f5166',
        'corp_code' : str(corp_code).rjust(8, '0')
    }

    res = requests.get(url, params = params)
    
    print(corp_name, res.ok)
    
    
    # 업종 코드를 저장하는 딕셔너리
    _dict = {}
    _dict['corp_name'] = corp_name
    _dict['corp_code'] = corp_code
    
    induty_code = res.json()['induty_code']
    _dict['업종코드'] = induty_code
    
    
    # 업종코드를 입력하여 대분류를 출력
    try:
        _dict['대분류'] = code_to_main_class[int(induty_code)]
        
    
    # 오류가 나는 경우 : 업종코드를 중분류 취급하여 입력하고, 대분류를 출력
    except:
        try:
            _dict['대분류'] = middle_class_to_main_class[int(induty_code)]
         
        # 그래도 오류가 나는 경우 : 대분류 None값으로
        except:
            _dict['대분류'] = None

    
    corp_induty_class.append(_dict)
    
df_corp_induty_class = pd.DataFrame(corp_induty_class)

list_corp_induty_code = df_corp_induty_class['업종코드']
list_main_category = df_corp_induty_class['대분류']

# 각 기업마다 대분류를 섹터로 바꿔줌

list_sector = []

for corp_name, corp_code, main_category, corp_induty_code in zip(list_corp_name, list_corp_code, list_main_category, list_corp_induty_code):
    if main_category == 'A':
        섹터 = '농업, 임업 및 어업'
        
    elif main_category == 'B':
        섹터 = '광업'
        
    elif main_category == 'C':
        
        try:
            middle_class = code_to_middle_class[int(corp_induty_code)]
        except:
            middle_class = int(corp_induty_code)
        
        if middle_class == 10:
            섹터 = '식료품'
            
        elif middle_class == 11:
            섹터 = '음료'
        
        elif middle_class == 13:
            섹터 = '섬유제품'
        
        elif middle_class == 14:
            섹터 = '의복'
            
        elif middle_class == 15:
            섹터 ='가죽 및 신발'
        
        elif middle_class == 16:
            섹터 = '목재 및 나무제품'
            
        elif middle_class == 18:
            섹터 = '인쇄 및 기록매체'
        
        elif middle_class == 22:
            섹터 = '고무 및 플라스틱'
            
        elif middle_class == 32:
            섹터 = '가구'
        
        elif middle_class in [12, 33]:
            섹터 = '경공업 기타'
            
        elif middle_class == 17:
            섹터 = '펄프 및 종이'
        
        elif middle_class == 20:
            섹터 = '화학제품'
            
        elif middle_class == 21:
            섹터 = '의약품'
            
        elif middle_class == 23:
            섹터 = '비금속광물'
            
        elif middle_class == 24:
            섹터 = '1차금속'

        elif middle_class == 25:
            섹터 = '금속가공'
    
        elif middle_class == 26:
            섹터 = '전자부품, 컴퓨터, 영상음향'
            
        elif middle_class == 27:
            섹터 = '의료, 정밀, 광학기기 및 시계'
            
        elif middle_class == 28:
            섹터 = '전기장비'
            
        elif middle_class == 29:
            섹터 = '기계장비'
            
        elif middle_class == 30:
            섹터 = '자동차 및 트레일러'
        
        elif middle_class == 31:
            섹터 = '기타 운송장비'
        
        elif middle_class == 19:
            섹터 = '중공업 기타'
            
        else:
            섹터 = '제조업 기타'
    
    elif main_category == 'D':
        섹터 = '전기, 가스, 증기 및 공기 조절 공급업'
        
    elif main_category == 'E':
        섹터 = '수도, 하수 및 폐기물 처리, 원료 재생업'
        
    elif main_category == 'F':
        섹터 = '건설업'
        
    elif main_category == 'G':
        섹터 = '도매 및 소매업'
        
    elif main_category == 'H':
        섹터 = '운수 및 창고업'
        
    elif main_category == 'I':
        섹터 = '숙박 및 음식점업'
        
    elif main_category == 'J':
        섹터 = '정보통신업'
        
    elif main_category == 'K':
        섹터 = '금융 및 보험업'
        
    elif main_category == 'L':
        섹터 = '부동산업'
        
    elif main_category == 'M':
        섹터 = '전문, 과학 및 기술 서비스업'
        
    elif main_category == 'N':
        섹터 = '사업시설 관리, 사업 지원 및 임대 서비스업'
        
    elif main_category == 'O':
        섹터 = '공공 행정, 국방 및 사회보장 행정'
        
    elif main_category == 'P':
        섹터 = '교육 서비스업'
        
    elif main_category == 'Q':
        섹터 = '보건업 및 사회복지 서비스업'
        
    elif main_category == 'R':
        섹터 = '예술, 스포츠 및 여가관련 서비스업'
        
    elif main_category == 'S':
        섹터 = '협회 및 단체, 수리 및 기타 개인 서비스업'
        
    elif main_category == 'T':
        섹터 = '가구 내 고용활동 및 달리 분류되지 않은 자가 소비 생산활동'
        
    elif main_category == 'U':
        섹터 = '국제 및 외국기관'
    
    else:
        섹터 = None
        
    
    each_sector = {
        'corp_name' : corp_name,
        'corp_code' : corp_code,
        '섹터' : 섹터
    }
    
    list_sector.append(each_sector)
    
df_sector = pd.DataFrame(list_sector)
corp_nps['섹터'] = df_sector['섹터']
corp_nps['업종코드'] = df_corp_induty_class['업종코드']
corp_nps.to_csv(f'corp_nps_{지역}_8.csv', encoding = 'cp949', index = False)
~~~

#### 데이터 결합 및 변수 생성
> 9.1_마지막 정제 및 통합.ipynb
1. 'corp_nps' 데이터를 활용하여 만들 수 있는 변수 feature 생성 
> 결과 데이터 : final_data_(지역).csv
~~~python
import pandas as pd
import numpy as np

corp_nps=pd.read_csv("corp_nps_(지역)_8.csv이 저장되어 있는 경로",encoding='cp949')

#1인당 월평균 납부하는 국민연금 금액
corp_nps["1인당 월 평균 납부하는 국민연금 금액"]=0
for i in range(1,13):
    month=str(i)+"월"
    corp_nps["1인당 월 평균 납부하는 국민연금 금액"]+=round(corp_nps[f'당월고지금액_{month}']/(corp_nps[f'가입자수_{month}']*12)) #1의 자리까지 반올림
    
#연평균 이직율
corp_nps["연간 퇴사자"]=0
for i in range(1,13):
    month=str(i)+"월"
    corp_nps["연간 퇴사자"]+=corp_nps[f'상실가입자수_{month}']
    
corp_nps["연 평균 재직인원"]=0
for j in range(1,13):
    month=str(j)+"월"
    corp_nps["연 평균 재직인원"]+=corp_nps[f'가입자수_{month}']
corp_nps["연 평균 재직인원"]=corp_nps["연 평균 재직인원"]/12
corp_nps["연간 이직율"]=corp_nps["연간 퇴사자"]/corp_nps["연 평균 재직인원"]*100

corp_nps=corp_nps[["corp_code","corp_name","대표자명","설립일자",'상세주소',"섹터","기업규모","주변 편의점 개수","정류장 개수","1인당 월 평균 납부하는 국민연금 금액","연간 이직율"]]

corp_nps["설립일자"].fillna(2023-12-31,inplace=True)
corp_nps["설립일자"]=corp_nps["설립일자"].astype(int)
corp_nps["설립일자"]=corp_nps["설립일자"].astype(str)

from datetime import datetime, timedelta

corp_nps['설립일자']=pd.to_datetime(corp_nps['설립일자'],format="%Y/%m/%d")
corp_nps['기준일']=pd.Timestamp(2021, 1, 1)
corp_nps["존속연수"]=(corp_nps['기준일'].dt.year-corp_nps['설립일자'].dt.year)
corp_nps.drop(["기준일"],axis=1,inplace=True)

data2=pd.read_csv("selected_feature(지역).csv이 저장되어 있는 경로",encoding='cp949')
data2.drop('비고',axis=1,inplace=True)
data2=data2.rename(columns={'corp_name':'corp_name_x'})
final_data=pd.concat([corp_nps,data2],axis=1)
final_data.drop('corp_name_x',axis=1,inplace=True)
final_data.to_csv("final_data_(지역).csv",encoding='cp949',index=False)
~~~
#### 데이터 통합
> 9_2_데이터 통합.ipynb
1. 각 지역별로 구분되어 있던 데이터를 하나의 데이터로 통합
> 결과 데이터 : 'final_data_전국.csv'
~~~python
import pandas as pd
data1=pd.read_csv("final_data_강원제주.csv",encoding='cp949')
data2=pd.read_csv("final_data_경기.csv",encoding='cp949')
data3=pd.read_csv("final_data_경상대구전라광주.csv",encoding='cp949')
data4=pd.read_csv("final_data_대전충청.csv",encoding='cp949')
data5=pd.read_csv("final_data_서울.csv",encoding='cp949')
data6=pd.read_csv("final_data_인천부산울산.csv",encoding='cp949')

integrated_data=pd.concat([data1,data2,data3,data4,data5,data6],axis=0)
integrated_data.to_csv("final_data_전국.csv",encoding="cp949",index=False)
~~~

#### 데이터 도산 여부 정의 및 sbhi 입력
> 10_조건 걸어서 도산 여부 판단하기, 섹터별 SBHI 가져오기.ipynb
1. 지역별 'final_data_(지역).csv'를 통합한 데이터를 활용
2. '도산' 기업을 정의하여 재분류
3. 섹터별로 'SBHI' 입력
> 결과 데이터 : 'final_data_2.csv'
~~~python
import pandas as pd
import numpy as np

final_data = pd.read_csv('final_data.csv가 저장되어 있는 경로', encoding = 'cp949')

##### 1. 조건 걸어서 도산 여부 판단하기 #####

# 도산 조건 1 : 완전자본잠식

final_data['자기자본회전율'] = final_data['자기자본회전율'].str.replace(',' , '' )
final_data['완전자본잠식 여부'] = (final_data['자기자본회전율'].apply(float) < 0).apply(int)

# 도산 조건 2 : 영업이익 마이너스

final_data['영업이익률'] = final_data['영업이익률'].str.replace(',' , '' )
final_data['영업이익 마이너스 여부'] = (final_data['영업이익률'].apply(float) < 0).apply(int)

# 도산 조건 3 : 영업이익증가율 마이너스

final_data['영업이익증가율'] = final_data['영업이익증가율'].str.replace(',', '')
final_data['영업이익증가율 마이너스 여부'] = (final_data['영업이익증가율'].apply(float) < 0).apply(int)

# 도산 조건 4 : 부채비율 500% 이상

final_data['부채비율'] = final_data['부채비율'].str.replace(',', '')
final_data['부채비율 500% 이상 여부'] = (final_data['부채비율'].apply(float) > 500).apply(int)

# 도산 조건 5 : 유동성비율 50% 이하

final_data['유동성비율'] = final_data['유동성비율'].str.replace(',', '')
final_data['유동성비율 50% 이하 여부'] = (final_data['유동성비율'].apply(float) < 50).apply(int)

list_corp_code = final_data['corp_code']
list_corp_name = final_data['corp_name']

list_dummy_1 = final_data['완전자본잠식 여부']
list_dummy_2 = final_data['영업이익 마이너스 여부']
list_dummy_3 = final_data['영업이익증가율 마이너스 여부']
list_dummy_4 = final_data['부채비율 500% 이상 여부']
list_dummy_5 = final_data['유동성비율 50% 이하 여부']

list_status = final_data['사업자 상태']

list_bankruptcy = []


# 폐업신고된 중소기업의 경우 5개 중 1개 조건,
# 계속사업중인 중소기업의 경우 5개 중 3개 조건에 해당하는 경우 도산으로 정의

for corp_code, corp_name, status, dummy_1, dummy_2, dummy_3, dummy_4, dummy_5 in zip(list_corp_code, list_corp_name, list_status, list_dummy_1, list_dummy_2, list_dummy_3, list_dummy_4, list_dummy_5):
    
    each_bankruptcy = {
        'corp_code' : corp_code,
        'corp_name' : corp_name,
    }
    
    
    bankruptcy_score = dummy_1 + dummy_2 + dummy_3 + dummy_4 + dummy_5
    
    
    if status == '정상':
        
        if bankruptcy_score >= 3:
            each_bankruptcy['도산'] = 1
        
        else:
            each_bankruptcy['도산'] = 0
            
    else:
        
        if bankruptcy_score >= 1:
            each_bankruptcy['도산'] = 1
        
        else:
            each_bankruptcy['도산'] = 0
        
    
    list_bankruptcy.append(each_bankruptcy)
    
df_bankruptcy = pd.DataFrame(list_bankruptcy)
final_data['도산'] = df_bankruptcy['도산']

# 더미변수 드랍

final_data.drop('완전자본잠식 여부', axis = 1, inplace = True)
final_data.drop('영업이익 마이너스 여부', axis = 1, inplace = True)
final_data.drop('영업이익증가율 마이너스 여부', axis = 1, inplace = True)
final_data.drop('부채비율 500% 이상 여부', axis = 1, inplace = True)
final_data.drop('유동성비율 50% 이하 여부', axis = 1, inplace = True)

##### 2. 섹터에 따라 SBHI 입력하기 #####

list_sector = final_data['섹터']

# 각 섹터의 SBHI를 딕셔너리로 대응

sector_to_sbhi = {
    '농업, 임업 및 어업' : 62.5, # 비제조업
    '광업' : 62.5, # 비제조업
    '식료품' : 73.3,
    '음료' : 82.8,
    '섬유제품' : 51.2,
    '의복' : 65.5,
    '가죽 및 신발' : 51.3,
    '목재 및 나무제품' : 66.3,
    '인쇄 및 기록매체' : 62.0,
    '고무 및 플라스틱' : 67.5,
    '가구' : 64.4,
    '경공업 기타' : 65.8, # 경공업
    '펄프 및 종이' : 67.6,
    '화학제품' : 75.9,
    '의약품' : 83.0,
    '비금속광물' : 68.4,
    '1차금속' : 72.2,
    '금속가공' : 72.1,
    '전자부품, 컴퓨터, 영상음향' : 78.9,
    '의료, 정밀, 광학기기 및 시계' : 73.8,
    '전기장비' : 68.3,
    '기계장비' : 73.6,
    '자동차 및 트레일러' : 72.6,
    '기타 운송장비' : 69.5,
    '중공업 기타' : 72.8, # 중공업
    '제조업 기타' : 70.6, # 제조업
    '전기, 가스, 증기 및 공기 조절 공급업' : 62.5, # 비제조업
    '수도, 하수 및 폐기물 처리, 원료 재생업' : 62.5, # 비제조업
    '건설업' : 70.7,
    '도매 및 소매업' : 58.6,
    '운수 및 창고업' : 63.0,
    '숙박 및 음식점업' : 48.9,
    '정보통신업' : 80.4,
    '금융 및 보험업' : 60.8, # 서비스업
    '부동산업' : 66.2,
    '전문, 과학 및 기술 서비스업' : 74.4,
    '공공 행정, 국방 및 사회보장 행정' : 60.8, # 서비스업
    '사업시설 관리, 사업 지원 및 임대 서비스업' : 72.8,
    '교육 서비스업' : 59.0,
    '보건업 및 사회복지 서비스업' : 60.8, # 서비스업
    '예술, 스포츠 및 여가관련 서비스업' : 62.3,
    '협회 및 단체, 수리 및 기타 개인 서비스업' : 60.3, 
    '가구 내 고용활동 및 달리 분류되지 않은 자가 소비 생산활동' : 65.3,  # 전산업
    '국제 및 외국기관' : 65.3,  # 전산업
}

list_sbhi = []

# 각 기업의 섹터에 대응되는 SBHI를 가져옴
for corp_code, corp_name, sector in zip(list_corp_code, list_corp_name, list_sector):
    
    try:
        sbhi = sector_to_sbhi[sector]
    except:
        sbhi = None
    
    each_sbhi = {
        'corp_code' : corp_code,
        'corp_name' : corp_name,
        'SBHI' : sbhi
    }
    
    list_sbhi.append(each_sbhi)
    
df_sbhi = pd.DataFrame(list_sbhi)
final_data['SBHI'] = df_sbhi['SBHI']
final_data.to_csv('final_data_2.csv', encoding = 'cp949', index = False)
~~~

## 데이터 전처리
#### 결측치 처리 및 설립일자 이상치 제거
> 11_5_결측치 처리.ipynb
1. 1인당 월 평균 국민연금 납부금액 null 이지만 연간 이직률이 null이 아닌 것들을 null로 처리
2. 섹터 null 값 '기타' 처리
3. SBHI null 값 '전 산업' SBHI 점수로 처리
4. 주변 편의점 개수, 정류장 개수의 null 값 각 지역 별 평균 값으로 대체
5. 1인당 월 평균 납부하는 국민연금 금액과 연간 이직률의 null 값 각 섹터의 평균 값으로 대체
6. 기업명과 대표자명이 같은 행 삭제
7. 설립일자 2020-01-01 이후 기업 삭제
> 결과 데이터 : 'final_data_3.csv'
~~~python
import pandas as pd
import numpy as np

final_data = pd.read_csv('final_data_2.csv가 저장되어 있는 경로', encoding = 'cp949')

## 1. 섹터 빈값 채우기
final_data['섹터'] =  final_data['섹터'].fillna('기타')

## 2. SBHI 빈값 채우기
# 전산업 SBHI로 대체

final_data['SBHI'] = final_data['SBHI'].fillna(65.3)

## 3. 주변 편의점 개수, 정류장 개수 빈값 채우기
list_index = final_data.loc[final_data['주변 편의점 개수'] == '조회 안됨']['주변 편의점 개수'].index
list_missing_value_address = final_data['상세주소'][list_index]
list_corp_code = final_data['corp_code']
list_corp_name = final_data['corp_name']
list_address = final_data['상세주소']
list_num_of_store = final_data['주변 편의점 개수']
list_num_of_station = final_data['정류장 개수']
list_missing_value = []


# 주변 편의점 개수와 정류장 개수가 결측된 기업들에 대해
# 그 인덱스와, 상세주소를 따 와서
for index, missing_value_address in zip(list_index, list_missing_value_address):
    
    try:
        count = 0
        sum_of_store = 0
        sum_of_station = 0
        
        
        # 관측치가 있는 모든 기업들에 대해 주소를 비교하고, 주소의 앞 두 자리가 같으면 편의점 개수와 정류장 개수를 합산한다
        for corp_code, corp_name, address, num_of_store, num_of_station in zip(list_corp_code, list_corp_name, list_address, list_num_of_store, list_num_of_station):
             if address.split()[0:2] == missing_value_address.split()[0:2]:
                if num_of_store != '조회 안됨':

                    count += 1
                    sum_of_store += float(num_of_store)
                    sum_of_station += float(num_of_station)
        
        # 결측된 기업과 주소의 앞 두 자리가 같은 기업들의 편의점 개수와 정류장 개수의 평균
        mean_of_store = sum_of_store / count
        mean_of_station = sum_of_station / count
        
        
    except:
        count = 0
        sum_of_store = 0
        sum_of_station = 0
        
        
        # 주소의 앞 두 자리가 같은 기업이 없는 경우, 주소의 앞 한 자리만 비교해서 합산한다
        for corp_code, corp_name, address, num_of_store, num_of_station in zip(list_corp_code, list_corp_name, list_address, list_num_of_store, list_num_of_station):
             if address.split()[0:1] == missing_value_address.split()[0:1]:
                if num_of_store != '조회 안됨':

                    count += 1
                    sum_of_store += float(num_of_store)
                    sum_of_station += float(num_of_station)

        mean_of_store = sum_of_store / count
        mean_of_station = sum_of_station / count
    
    
    missing_value = {
        'index' : index,
        'store_value' : mean_of_store,
        'station_value' : mean_of_station
    }
    
    list_missing_value.append(missing_value)
    
df_missing_value = pd.DataFrame(list_missing_value)
df_missing_value.set_index('index')
# 결측치를 대체할 값들을 삽입한다

final_data['주변 편의점 개수'][list_index] = df_missing_value['store_value']
final_data['정류장 개수'][list_index] = df_missing_value['station_value']

## 4. 1인당 월 평균 납부하는 국민연금 금액 빈값 채우기
final_data.loc[final_data['1인당 월 평균 납부하는 국민연금 금액'].isnull()]['1인당 월 평균 납부하는 국민연금 금액']
list_index = final_data.loc[final_data['1인당 월 평균 납부하는 국민연금 금액'].isnull()].index
list_sector = final_data['섹터'][list_index]
nps_amount_not_null_condition = final_data['1인당 월 평균 납부하는 국민연금 금액'].notnull()
list_missing_value = []


# 1인당 월 평균 납부하는 국민연금 금액이 결측된 기업들에 대해
# 그 기업들의 인덱스와, 섹터를 가져와서
for index, sector in zip(list_index, list_sector):
    
    # 그 기업들과 동일한 섹터에 속한 기업들의 1인당 월 평균 납부하는 국민연금 금액의 평균을 구해준다
    sector_condition = final_data['섹터'] == sector
    value = final_data.loc[nps_amount_not_null_condition & sector_condition]['1인당 월 평균 납부하는 국민연금 금액'].mean()
    
    missing_value = {
        'index' : index,
        'value' : value
    }
    
    list_missing_value.append(missing_value)
    
df_missing_value = pd.DataFrame(list_missing_value)
# 결측치를 대체할 값을 삽입한다

final_data['1인당 월 평균 납부하는 국민연금 금액'][list_index] = df_missing_value['value']

## 5. 연간 이직률 빈칸 채우기
final_data.loc[final_data['연간 이직율'].isnull()]['연간 이직율']
list_index = final_data.loc[final_data['연간 이직율'].isnull()].index
list_sector = final_data['섹터'][list_index]
nps_turnover_not_null_condition = final_data['연간 이직율'].notnull()
list_missing_value = []


# 연간 이직률이 결측된 기업들에 대해
# 그 기업의 인덱스와 섹터를 따 와서
for index, sector in zip(list_index, list_sector):
    
    # 같은 섹터에 속한 기업들의 연간 이직률의 평균을 구한다
    sector_condition = final_data['섹터'] == sector
    value = final_data.loc[nps_turnover_not_null_condition & sector_condition]['연간 이직율'].mean()
    
    missing_value = {
        'index' : index,
        'value' : value
    }
    
    list_missing_value.append(missing_value)
    
df_missing_value = pd.DataFrame(list_missing_value)
final_data['연간 이직율'][list_index] = df_missing_value['value']
final_data.to_csv('final_data_3.csv', encoding = 'cp949', index = False)
~~~

#### feature 보정 및 데이터 선정
> 12_변수 보정하고 독립변수와 종속변수만 남기기.ipynb
1. 편의점 개수, 정류장 개수, 연간 이직율, 존속연수 루트 스케일링 
2. 부채비율을 제외한 재무비율의 경우, 양수값에 대해서는 해당값과 제 99 분위수 중 작은 값의 루트값, 음수값은 해당 값과 제 1 분위수 중 큰 값의 절댓값의 루트값의 음수값
3. 부채비율의 경우, 양수값은 해당 값과 제 99 분위수 중 작은 값의 루트값, 음수값은 제 99 분위수의 루트값
> 결과 데이터 : 'model_data.csv'
~~~python
import pandas as pd
import numpy as np

final_data = pd.read_csv('final_data_3.csv가 저장되어 있는 경로', encoding = 'cp949', thousands = ',')

model_data = pd.DataFrame(final_data[['corp_code', 'corp_name']])

# 1. 1인당 월 평균 납부하는 국민연금 금액, SBHI
# 그대로 입력
model_data =  pd.concat([model_data, final_data.iloc[:, [9, 30]]], axis = 1)

# 2. 주변 편의점 개수, 정류장 개수, 연간 이직율, 존속연수
# 루트 처리

def sqrt_revision(x):
    if x < 0:
        x = -np.sqrt(abs(x))
    
    else:
        x = np.sqrt(x)
    
    return(x)
    
for num in [7, 8, 10, 11]:
    model_data = pd.concat([model_data, final_data.iloc[:, num].apply(sqrt_revision)], axis = 1)
    
# 3. 부채비율을 제외한 재무비율
# 양수의 경우 : 해당 값과 제 99 분위수 중 작은 값의 루트값
# 음수의 경우 : 해당 값과 제 1 분위수 중 큰 값의 절대값의 루트값의 음수

def sqrt_revision(x):
    if x < 0:
        x = -np.sqrt(abs(max(x, lower_quantile)))
    
    else:
        x = np.sqrt(min(x, upper_quantile))
    
    return(x)
    
for num in [12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 23, 24]:
    
    upper_quantile = final_data.iloc[:, num].quantile(0.99)
    lower_quantile = final_data.iloc[:, num].quantile(0.01)
    
    model_data = pd.concat([model_data, final_data.iloc[:, num].apply(sqrt_revision)], axis = 1)
    
# 4. 부채비율
# 양수의 경우 해당 값과 제 99 분위수 중 작은 값의 루트값
# 음수의 경우 제 99 분위수의 루트값

def sqrt_limit_revision(x):
    if x <= 0:
        x = np.sqrt(upper_quantile)
    
    else:
        x = np.sqrt(min(x, upper_quantile))
    
    return(x)
    
upper_quantile = final_data.iloc[:, 22].quantile(0.99)
model_data = pd.concat([model_data, final_data.iloc[:, 22].apply(sqrt_limit_revision)], axis = 1)

# 5. target 붙이기
model_data = pd.concat([model_data, final_data['도산']], axis = 1)
model_data.to_csv('model_data.csv', encoding = 'cp949', index = False)
~~~

## 모델링
#### 재무 feature와 비재무 feature 결합 모델링
> 재무 feature와 비재무 feature를 결합한 데이터에 대한 모델링 진행
##### 상관관계 높은 개별 feature에 pca
> 13_1_상관관계 높은 개별 feature에 PCA하기.ipynb
~~~python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

x_scaled = pd.read_csv('x_scaled.csv가 저장되어 있는 경로', encoding = 'cp949')

## PCA를 통한 차원 축소 : 다중공선성이 발생하는 feature들을 중심으로
from sklearn.decomposition import PCA

# scree plot

def scree_plot(pca):
    num_components = len(pca.explained_variance_ratio_)
    ind = np.arange(num_components)
    vals = pca.explained_variance_ratio_ 
    
    ax = plt.subplot()
    cumvals = np.cumsum(vals)
    ax.bar(ind, vals) # Bar plot
    ax.plot(ind, cumvals, color = '#c0392b') # Line plot 
    
    for i in range(num_components): #라벨링(바 위에 텍스트(annotation) 쓰기)
        ax.annotate(r"%s" % ((str(vals[i]*100)[:3])), (ind[i], vals[i]), va = "bottom", ha = "center", fontsize = 13)
    
    ax.set_xlabel("PC")
    ax.set_ylabel("Variance")
    plt.title('Scree plot')

# 1. 주변 편의점 개수 & 정류장 개수
data_1 = x_scaled[['주변 편의점 개수', '정류장 개수']]
pca = PCA(n_components = 2)
pc_1 = pca.fit_transform(data_1)
df_pc_1 = pd.DataFrame(data = pc_1)
df_pc_1 = pd.DataFrame(df_pc_1)
df_pc_1.columns = ['접근성 PC1']

# 2. 순이익률, 영업이익률, 매출총이익률, 총자산이익률, 자본금이익률
data_2 = x_scaled[['순이익률', '영업이익률', '매출총이익률', '총자산순이익률(ROA)', '자본금이익률(ROE)']]
pca = PCA(n_components = 5)
pc_2 = pca.fit_transform(data_2)
df_pc_2 = pd.DataFrame(data = pc_2)

scree_plot(pca)  # PC1, PC2가 변동의 83%를 설명

df_pc_2 = df_pc_2.iloc[:, 0:2]
df_pc_2.columns = ['수익성 PC1', '수익성 PC2']

# 3. 영업이익증가율, 순이익증가율
data_3 = x_scaled[['영업이익증가율', '순이익증가율']]
pca = PCA(n_components = 2)
pc_3 = pca.fit_transform(data_3)
df_pc_3 = pd.DataFrame(data = pc_3)
df_pc_3 = df_pc_3.iloc[:, 0]
df_pc_3 = pd.DataFrame(df_pc_3)
df_pc_3.columns = ['이익증가율 PC1']

# 4. 총자본회전율, 자기자본회전율
data_4 = x_scaled[['총자본회전율', '자기자본회전율']]
pca = PCA(n_components = 2)
pc_4 = pca.fit_transform(data_4)
df_pc_4 = pd.DataFrame(data = pc_4)
scree_plot(pca)  # PC1이 변동의 83%를 설명
df_pc_4 = df_pc_4.iloc[:, 0]
df_pc_4 = pd.DataFrame(df_pc_4)
df_pc_4.columns = ['활동성 PC1']

# 5. 유동성비율, 당좌비율
data_5 = x_scaled[['유동성비율', '당좌비율']]
pca = PCA(n_components = 2)
pc_5 = pca.fit_transform(data_5)
df_pc_5 = pd.DataFrame(data = pc_5)
scree_plot(pca)  # PC1이 변동의 97%를 설명
df_pc_5 = df_pc_5.iloc[:, 0]
df_pc_5 = pd.DataFrame(df_pc_5)
df_pc_5.columns = ['안정성 PC1']

x_scaled = x_scaled.drop(['주변 편의점 개수', '정류장 개수', '순이익률', '영업이익률', '매출총이익률', '총자산순이익률(ROA)', '자본금이익률(ROE)', '영업이익증가율', '순이익증가율', '총자본회전율', '자기자본회전율', '유동성비율', '당좌비율'], axis = 1)
x_scaled = pd.concat([x_scaled, df_pc_1, df_pc_2, df_pc_3, df_pc_4, df_pc_5], axis = 1)

x_scaled.to_csv('x_scaled_with_pca.csv', encoding = 'cp949', index = False)
~~~
##### 로지스틱 모델링
> 13_2_로지스틱 모델링.ipynb
~~~python
import pandas as pd
import numpy as np

from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
from sklearn import metrics
from sklearn.metrics import confusion_matrix
from sklearn.metrics import accuracy_score, roc_auc_score, roc_curve, precision_recall_curve

import matplotlib.pyplot as plt

# 개별 feature PCA 한 데이터 가져오기

x_scaled = pd.read_csv('x_scaled_with_pca.csv가 저장되어 있는 경로', encoding = 'cp949')

# target 가져오기

model_data = pd.read_csv('model_data.csv가 저장되어 있는 경로', encoding = 'cp949', thousands = ',')

model_data.drop(['corp_code', 'corp_name'], axis = 1, inplace = True)

y_data = model_data['도산']

# 훈련-시험 데이터 분할
x_train, x_test, y_train, y_test = train_test_split(x_scaled, y_data, 
                                                     train_size = 0.8,
                                                     stratify = y_data)
                                                     
# 데이터 증강
from sklearn.datasets import make_classification
from imblearn.over_sampling import SMOTE

smote = SMOTE(sampling_strategy = 1, k_neighbors = 5)
x_train_r, y_train_r = smote.fit_resample(x_train, y_train)

lr_clf = LogisticRegression()
lr_clf.fit(x_train_r, y_train_r)
y_pred = lr_clf.predict_proba(x_test)[:, 1]

# ROC Curve

fpr, tpr, thresholds = metrics.roc_curve(y_test, y_pred)

plt.plot(fpr, tpr)

auc = np.trapz(tpr, fpr)
print('AUC : ', auc)

precision, recall, thresholds = precision_recall_curve(y_test, y_pred)

f1_scores = 2*recall*precision/(recall+precision)
print('Best threshold: ', thresholds[np.argmax(f1_scores)])
print('Best F1-Score: ', np.max(f1_scores))

# statsmodel로 summary 보기
import statsmodels.api as sm

model = sm.Logit(y_train_r, x_train_r)
results = model.fit(method = 'newton')
results.summary()
~~~

##### svm
> 13_3_SVM.ipynb
~~~python
import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn import metrics
from sklearn.metrics import confusion_matrix
from sklearn.metrics import accuracy_score, roc_auc_score, roc_curve, precision_recall_curve

import matplotlib.pyplot as plt

# 개별 feature PCA 한 데이터 가져오기

x_scaled = pd.read_csv('x_scaled_with_pca.csv가 저장되어 있는 경로', encoding = 'cp949')

# target 가져오기

model_data = pd.read_csv('model_data.csv가 저장되어 있는 경로', encoding = 'cp949', thousands = ',')

model_data.drop(['corp_code', 'corp_name'], axis = 1, inplace = True)

y_data = model_data['도산']

# 훈련-시험 데이터 분할
x_train, x_test, y_train, y_test = train_test_split(x_scaled, y_data, 
                                                     train_size = 0.8,
                                                     stratify = y_data)
                                                     
# 데이터 증강
from sklearn.datasets import make_classification
from imblearn.over_sampling import SMOTE

smote = SMOTE(sampling_strategy = 1, k_neighbors = 5)
x_train_r, y_train_r = smote.fit_resample(x_train, y_train)

from sklearn import svm
# kernel = rbf, C = 0.05
clf = svm.SVC(kernel = 'rbf', C = 0.05, probability = True)
clf.fit(x_train_r, y_train_r)
y_pred = clf.predict_proba(x_test)[: , 1]


# ROC Curve

fpr, tpr, thresholds = metrics.roc_curve(y_test, y_pred)

plt.plot(fpr, tpr)

auc = np.trapz(tpr, fpr)
print('AUC : ', auc)

precision, recall, thresholds = precision_recall_curve(y_test, y_pred)
f1_scores = 2*recall*precision/(recall+precision)
print('Best threshold: ', thresholds[np.argmax(f1_scores)])
print('Best F1-Score: ', np.max(f1_scores))

# kernel = linear, C = 0.05
clf = svm.SVC(kernel = 'linear', C = 0.05, probability = True)
clf.fit(x_train_r, y_train_r)
y_pred = clf.predict_proba(x_test)[: , 1]

# ROC Curve

fpr, tpr, thresholds = metrics.roc_curve(y_test, y_pred)

plt.plot(fpr, tpr)

auc = np.trapz(tpr, fpr)
print('AUC : ', auc)

precision, recall, thresholds = precision_recall_curve(y_test, y_pred)
f1_scores = 2*recall*precision/(recall+precision)
print('Best threshold: ', thresholds[np.argmax(f1_scores)])
print('Best F1-Score: ', np.max(f1_scores))

# kernel = rbf, C = 0.1
clf = svm.SVC(kernel = 'rbf', C = 0.1, probability = True)
clf.fit(x_train_r, y_train_r)
y_pred = clf.predict_proba(x_test)[: , 1]

# ROC Curve

fpr, tpr, thresholds = metrics.roc_curve(y_test, y_pred)

plt.plot(fpr, tpr)

auc = np.trapz(tpr, fpr)
print('AUC : ', auc)

precision, recall, thresholds = precision_recall_curve(y_test, y_pred)
f1_scores = 2*recall*precision/(recall+precision)
print('Best threshold: ', thresholds[np.argmax(f1_scores)])
print('Best F1-Score: ', np.max(f1_scores))

# kernel = linear, C = 0.1
clf = svm.SVC(kernel = 'linear', C = 0.1, probability = True)
clf.fit(x_train_r, y_train_r)
y_pred = clf.predict_proba(x_test)[: , 1]

# ROC Curve

fpr, tpr, thresholds = metrics.roc_curve(y_test, y_pred)

plt.plot(fpr, tpr)

auc = np.trapz(tpr, fpr)
print('AUC : ', auc)

precision, recall, thresholds = precision_recall_curve(y_test, y_pred)
f1_scores = 2*recall*precision/(recall+precision)
print('Best threshold: ', thresholds[np.argmax(f1_scores)])
print('Best F1-Score: ', np.max(f1_scores))

# kernel = rbf, C = 0.5
clf = svm.SVC(kernel = 'rbf', C = 0.5, probability = True)
clf.fit(x_train_r, y_train_r)
y_pred = clf.predict_proba(x_test)[: , 1]

# ROC Curve

fpr, tpr, thresholds = metrics.roc_curve(y_test, y_pred)

plt.plot(fpr, tpr)

auc = np.trapz(tpr, fpr)
print('AUC : ', auc)

precision, recall, thresholds = precision_recall_curve(y_test, y_pred)
f1_scores = 2*recall*precision/(recall+precision)
print('Best threshold: ', thresholds[np.argmax(f1_scores)])
print('Best F1-Score: ', np.max(f1_scores))

# kernel = linear, C = 0.5
clf = svm.SVC(kernel = 'linear', C = 0.5, probability = True)
clf.fit(x_train_r, y_train_r)
y_pred = clf.predict_proba(x_test)[: , 1]

# ROC Curve

fpr, tpr, thresholds = metrics.roc_curve(y_test, y_pred)

plt.plot(fpr, tpr)

auc = np.trapz(tpr, fpr)
print('AUC : ', auc)

precision, recall, thresholds = precision_recall_curve(y_test, y_pred)
f1_scores = 2*recall*precision/(recall+precision)
print('Best threshold: ', thresholds[np.argmax(f1_scores)])
print('Best F1-Score: ', np.max(f1_scores))

# kernel = rbf, C = 1
clf = svm.SVC(kernel = 'rbf', C = 1, probability = True)
clf.fit(x_train_r, y_train_r)
y_pred = clf.predict_proba(x_test)[: , 1]

# ROC Curve

fpr, tpr, thresholds = metrics.roc_curve(y_test, y_pred)

plt.plot(fpr, tpr)

auc = np.trapz(tpr, fpr)
print('AUC : ', auc)

precision, recall, thresholds = precision_recall_curve(y_test, y_pred)
f1_scores = 2*recall*precision/(recall+precision)
print('Best threshold: ', thresholds[np.argmax(f1_scores)])
print('Best F1-Score: ', np.max(f1_scores))

# kernel = rbf, C = 5
clf = svm.SVC(kernel = 'rbf', C = 5, probability = True)
clf.fit(x_train_r, y_train_r)
y_pred = clf.predict_proba(x_test)[: , 1]

# ROC Curve

fpr, tpr, thresholds = metrics.roc_curve(y_test, y_pred)

plt.plot(fpr, tpr)

auc = np.trapz(tpr, fpr)
print('AUC : ', auc)

precision, recall, thresholds = precision_recall_curve(y_test, y_pred)
f1_scores = 2*recall*precision/(recall+precision)
print('Best threshold: ', thresholds[np.argmax(f1_scores)])
print('Best F1-Score: ', np.max(f1_scores))

# kernel = rbf, C = 10
clf = svm.SVC(kernel = 'rbf', C = 10, probability = True)
clf.fit(x_train_r, y_train_r)
y_pred = clf.predict_proba(x_test)[: , 1]
# ROC Curve

fpr, tpr, thresholds = metrics.roc_curve(y_test, y_pred)

plt.plot(fpr, tpr)

auc = np.trapz(tpr, fpr)
print('AUC : ', auc)

precision, recall, thresholds = precision_recall_curve(y_test, y_pred)
f1_scores = 2*recall*precision/(recall+precision)
print('Best threshold: ', thresholds[np.argmax(f1_scores)])
print('Best F1-Score: ', np.max(f1_scores))

# kernel = rbf, C = 1 결정
~~~

##### 의사결정트리
> 13_4 Decision Tree.ipynb
~~~python
import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn import metrics
from sklearn.metrics import confusion_matrix
from sklearn.metrics import accuracy_score, roc_auc_score, roc_curve, precision_recall_curve

import matplotlib.pyplot as plt

# 개별 feature PCA 한 데이터 가져오기

x_scaled = pd.read_csv('x_scaled_with_pca.csv가 저장되어 있는 경로', encoding = 'cp949')

# target 가져오기

model_data = pd.read_csv('model_data.csv가 저장되어 있는 경로', encoding = 'cp949', thousands = ',')

model_data.drop(['corp_code', 'corp_name'], axis = 1, inplace = True)

y_data = model_data['도산']

# 훈련-시험 데이터 분할
x_train, x_test, y_train, y_test = train_test_split(x_scaled, y_data, 
                                                     train_size = 0.8,
                                                     stratify = y_data)
                                                     
# 데이터 증강
from sklearn.datasets import make_classification
from imblearn.over_sampling import SMOTE

smote = SMOTE(sampling_strategy = 1, k_neighbors = 5)
x_train_r, y_train_r = smote.fit_resample(x_train, y_train)

# max_depth 조절하면서 roc curve, f1-score 보기
from sklearn import tree

score = []

for i in range(3, 20):
    clf = tree.DecisionTreeClassifier(max_depth = i)
    clf.fit(x_train_r, y_train_r)
    
    y_pred = clf.predict_proba(x_test)[:, 1]
    
    fpr, tpr, thresholds = metrics.roc_curve(y_test, y_pred)
    precision, recall, thresholds = precision_recall_curve(y_test, y_pred)
    
    auc = np.trapz(tpr, fpr)
    
    f1_scores = 2*recall*precision/(recall+precision)
    
    best_threshold = thresholds[np.argmax(f1_scores)]
    best_f1_score = np.max(f1_scores)
    
    _dict = {
        'auc' : auc,
        'best_threshold' : best_threshold,
        'best_f1_score' : best_f1_score
    }
    
    score.append(_dict)
    
df_score = pd.DataFrame(score)
df_score.index = range(3, 20)

plt.plot(df_score['auc'])
plt.plot(df_score['best_f1_score'])
# 여러번 시행했을 때, max_depth = 6 정도가 적절해 보임
~~~

##### knn
> 13_5_kNN.ipynb
~~~python
import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn import metrics
from sklearn.metrics import confusion_matrix
from sklearn.metrics import accuracy_score, roc_auc_score, roc_curve, precision_recall_curve

import matplotlib.pyplot as plt

# 개별 feature PCA 한 데이터 가져오기

x_scaled = pd.read_csv('x_scaled_with_pca.csv가 저장되어 있는 경로', encoding = 'cp949')

# target 가져오기

model_data = pd.read_csv('model_data.csv가 저장되어 있는 경로', encoding = 'cp949', thousands = ',')

model_data.drop(['corp_code', 'corp_name'], axis = 1, inplace = True)

y_data = model_data['도산']

# 훈련-시험 데이터 분할
x_train, x_test, y_train, y_test = train_test_split(x_scaled, y_data, 
                                                     train_size = 0.8,
                                                     stratify = y_data)
                                                     
# 데이터 증강
from sklearn.datasets import make_classification
from imblearn.over_sampling import SMOTE

smote = SMOTE(sampling_strategy = 1, k_neighbors = 5)
x_train_r, y_train_r = smote.fit_resample(x_train, y_train)

from sklearn.neighbors import KNeighborsClassifier
# n_neighbors 조절하면서 auc, f1-score 보기

score = []

for i in range(1, 100):
    clf = KNeighborsClassifier(i)
    clf.fit(x_train_r, y_train_r)
    
    y_pred = clf.predict_proba(x_test)[:, 1]
    
    fpr, tpr, thresholds = metrics.roc_curve(y_test, y_pred)
    precision, recall, thresholds = precision_recall_curve(y_test, y_pred)
    
    auc = np.trapz(tpr, fpr)
    
    f1_scores = 2*recall*precision/(recall+precision)
    
    best_threshold = thresholds[np.argmax(f1_scores)]
    best_f1_score = np.max(f1_scores)
    
    _dict = {
        'auc' : auc,
        'best_threshold' : best_threshold,
        'best_f1_score' : best_f1_score
    }
    
    score.append(_dict)
    
df_score = pd.DataFrame(score)
df_score.index = range(1, 100)

plt.plot(df_score['auc'])
plt.plot(df_score['best_f1_score'])
# 시행마다 그래프의 형태가 매우 다름. 그나마 n_neighbors = 35 정도가 무난할 것 같음
~~~

##### 앙상블_보팅
> 13_6_Ensemble Method_Voting.ipynb
~~~python
import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn import metrics
from sklearn.metrics import confusion_matrix
from sklearn.metrics import accuracy_score, roc_auc_score, roc_curve, precision_recall_curve


import matplotlib.pyplot as plt

# 개별 feature PCA 한 데이터 가져오기

x_scaled = pd.read_csv('x_scaled_with_pca.csv가 저장되어 있는 경로', encoding = 'cp949')

# target 가져오기

model_data = pd.read_csv('model_data.csv가 저장되어 있는 경로', encoding = 'cp949', thousands = ',')

model_data.drop(['corp_code', 'corp_name'], axis = 1, inplace = True)

y_data = model_data['도산']

# 훈련-시험 데이터 분할
x_train, x_test, y_train, y_test = train_test_split(x_scaled, y_data, 
                                                     train_size = 0.8,
                                                     stratify = y_data)
                                                     
# 데이터 증강
from sklearn.datasets import make_classification
from imblearn.over_sampling import SMOTE

smote = SMOTE(sampling_strategy = 1, k_neighbors = 5)
x_train_r, y_train_r = smote.fit_resample(x_train, y_train)

## 1. 보팅 앙상블 기법 적용
from sklearn.ensemble import VotingClassifier
from sklearn.linear_model import LogisticRegression
from sklearn import svm
from sklearn import tree
from sklearn.neighbors import KNeighborsClassifier

# 기존 최적화했던 하이퍼 파라미터 적용

lr_clf = LogisticRegression()
svm_clf = svm.SVC(kernel = 'rbf', C = 1, probability = True)
dt_clf = tree.DecisionTreeClassifier(max_depth = 6)
knn_clf = KNeighborsClassifier(n_neighbors = 35)

# 소프트 보팅
svot_clf = VotingClassifier(estimators = [('Logistic', lr_clf), ('SVM', svm_clf), ('DT', dt_clf), ('kNN', knn_clf)],
                            voting = 'soft')
svot_clf.fit(x_train_r, y_train_r)
svot_clf_pred = svot_clf.predict(x_test)
print(accuracy_score(y_test, svot_clf_pred))

# threshold 조절해서 ROC curve 그려보기
y_pred = svot_clf.predict_proba(x_test)[: , 1]

# ROC Curve :

fpr, tpr, thresholds = metrics.roc_curve(y_test, y_pred)

plt.plot(fpr, tpr)

auc = np.trapz(tpr, fpr)
print('AUC : ', auc)

# f1_score의 최댓값과 그 때의 threshold 찾기
precision, recall, thresholds = precision_recall_curve(y_test, y_pred)
f1_scores = 2*recall*precision/(recall+precision)
print('Best threshold: ', thresholds[np.argmax(f1_scores)])
print('Best F1-Score: ', np.max(f1_scores))
~~~

##### 앙상블_랜덤 포레스트
> 13_7_Ensemble Method_Random Forest.ipynb
~~~python
import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn import metrics
from sklearn.metrics import confusion_matrix
from sklearn.metrics import accuracy_score, roc_auc_score, roc_curve, precision_recall_curve

import matplotlib.pyplot as plt

# 개별 feature PCA 한 데이터 가져오기

x_scaled = pd.read_csv('x_scaled_with_pca.csv가 저장되어 있는 경로', encoding = 'cp949')

# target 가져오기

model_data = pd.read_csv('model_data.csv가 저장되어 있는 경로', encoding = 'cp949', thousands = ',')

model_data.drop(['corp_code', 'corp_name'], axis = 1, inplace = True)
y_data = model_data['도산']

# 훈련-시험 데이터 분할
x_train, x_test, y_train, y_test = train_test_split(x_scaled, y_data, 
                                                     train_size = 0.8,
                                                     stratify = y_data)
# 데이터 증강
from sklearn.datasets import make_classification
from imblearn.over_sampling import SMOTE

smote = SMOTE(sampling_strategy = 1, k_neighbors = 5)
x_train_r, y_train_r = smote.fit_resample(x_train, y_train)

from sklearn.ensemble import RandomForestClassifier
# max_depth 조절하면서 auc, f1-score 보기
score = []

for i in range(5, 40):
    rf_clf = RandomForestClassifier(n_estimators = 1000,
                                    max_depth = i,
                                    max_features = 'auto',
                                    verbose = 1,
                                    n_jobs = -1)
    
    rf_clf.fit(x_train_r, y_train_r)
    y_pred = rf_clf.predict_proba(x_test)[: , 1]
    
    fpr, tpr, thresholds = metrics.roc_curve(y_test, y_pred)
    precision, recall, thresholds = precision_recall_curve(y_test, y_pred)
    
    auc = np.trapz(tpr, fpr)
    
    f1_scores = 2*recall*precision/(recall+precision)
    
    best_threshold = thresholds[np.argmax(f1_scores)]
    best_f1_score = np.max(f1_scores)
    
    _dict = {
        'auc' : auc,
        'best_threshold' : best_threshold,
        'best_f1_score' : best_f1_score
    }
    
    score.append(_dict)
    
df_score = pd.DataFrame(score)
df_score.index = range(5, 40)

plt.plot(df_score['auc'])
plt.plot(df_score['best_f1_score'])

## 20개 이상 정도면 적당한 것 같음

rf_clf = RandomForestClassifier(n_estimators = 1000,
                                    max_depth = 25,
                                    max_features = 'auto',
                                    verbose = 1,
                                    n_jobs = -1)
    
rf_clf.fit(x_train_r, y_train_r)
# feature 중요도 시각화
def plot_feature_importance(model):
    n_features = x_scaled.shape[1]
    plt.barh(np.arange(n_features), sorted(model.feature_importances_), align="center")
    plt.yticks(np.arange(n_features), x_scaled.columns)
    plt.xlabel("Random Forest Feature Importance")
    plt.ylabel("Feature")
    plt.ylim(-1, n_features)

plt.rc('font', family = 'Malgun Gothic')
plot_feature_importance(rf_clf)
~~~

##### 앙상블_xgboost
>13_8_Ensemble Method_XGBoost.ipynb
~~~python
import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn import metrics
from sklearn.metrics import confusion_matrix
from sklearn.metrics import accuracy_score, roc_auc_score, roc_curve, precision_recall_curve

import matplotlib.pyplot as plt

# 개별 feature PCA 한 데이터 가져오기

x_scaled = pd.read_csv('x_scaled_with_pca.csv가 저장되어 있는 경로', encoding = 'cp949')

# target 가져오기

model_data = pd.read_csv('model_data.csv가 저장되어 있는 경로', encoding = 'cp949', thousands = ',')

model_data.drop(['corp_code', 'corp_name'], axis = 1, inplace = True)
y_data = model_data['도산']

# 훈련-시험 데이터 분할
x_train, x_test, y_train, y_test = train_test_split(x_scaled, y_data, 
                                                     train_size = 0.8,
                                                     stratify = y_data)
# 데이터 증강
from sklearn.datasets import make_classification
from imblearn.over_sampling import SMOTE

smote = SMOTE(sampling_strategy = 1, k_neighbors = 5)
x_train_r, y_train_r = smote.fit_resample(x_train, y_train)

# DMatrix 변환
dtrain = xgb.DMatrix(data = x_train_r, label = y_train_r)
dtest = xgb.DMatrix(data = x_test, label = y_test)

wlist = [(dtrain, 'train'), (dtest, 'eval')]

## max_depth, eta, num_boost_round 바꾸면서 f1-score, auc 보기 -> 대체적으로 7개가 적합해보임
# eta = 0.05, num_boost_round = 500

grid = []

for max_depth in [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]:    
    params = {'max_depth' : max_depth,
             'eta' : 0.05, 
             'objective' : 'binary:logistic',
             'eval_metric' : 'logloss',
             'early_stoppings' : 50 }
    
    xgb_model = xgb.train(params = params, dtrain = dtrain, num_boost_round = 500, evals = wlist)
    xgb_model_predict = xgb_model.predict(dtest)
    
    fpr, tpr, thresholds = metrics.roc_curve(y_test, xgb_model_predict)
    precision, recall, thresholds = precision_recall_curve(y_test, xgb_model_predict)
    f1_scores = 2*recall*precision/(recall+precision)
    
    
    _dict = {
        'max_depth' : max_depth,
        'best threshold' : thresholds[np.argmax(f1_scores)],
        'best F1-score' : np.max(f1_scores),
        'auc' : np.trapz(tpr, fpr)
    }

    grid.append(_dict)
    
pd.DataFrame(grid)

# eta = 0.1, num_boost_round = 500

grid = []

for max_depth in [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]:    
    params = {'max_depth' : max_depth,
             'eta' : 0.1, 
             'objective' : 'binary:logistic',
             'eval_metric' : 'logloss',
             'early_stoppings' : 50 }
    
    xgb_model = xgb.train(params = params, dtrain = dtrain, num_boost_round = 500, evals = wlist)
    xgb_model_predict = xgb_model.predict(dtest)
    
    fpr, tpr, thresholds = metrics.roc_curve(y_test, xgb_model_predict)
    precision, recall, thresholds = precision_recall_curve(y_test, xgb_model_predict)
    f1_scores = 2*recall*precision/(recall+precision)
    
    
    _dict = {
        'max_depth' : max_depth,
        'best threshold' : thresholds[np.argmax(f1_scores)],
        'best F1-score' : np.max(f1_scores),
        'auc' : np.trapz(tpr, fpr)
    }

    grid.append(_dict)
    
pd.DataFrame(grid)

# eta = 0.15, num_boost_round = 500

grid = []

for max_depth in [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]:    
    params = {'max_depth' : max_depth,
             'eta' : 0.15, 
             'objective' : 'binary:logistic',
             'eval_metric' : 'logloss',
             'early_stoppings' : 50 }
    
    xgb_model = xgb.train(params = params, dtrain = dtrain, num_boost_round = 500, evals = wlist)
    xgb_model_predict = xgb_model.predict(dtest)
    
    fpr, tpr, thresholds = metrics.roc_curve(y_test, xgb_model_predict)
    precision, recall, thresholds = precision_recall_curve(y_test, xgb_model_predict)
    f1_scores = 2*recall*precision/(recall+precision)
    
    
    _dict = {
        'max_depth' : max_depth,
        'best threshold' : thresholds[np.argmax(f1_scores)],
        'best F1-score' : np.max(f1_scores),
        'auc' : np.trapz(tpr, fpr)
    }

    grid.append(_dict)
    
 pd.DataFrame(grid)
 
 # eta = 0.2, num_boost_round = 500
 
 grid = []

for max_depth in [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]:    
    params = {'max_depth' : max_depth,
             'eta' : 0.2, 
             'objective' : 'binary:logistic',
             'eval_metric' : 'logloss',
             'early_stoppings' : 50 }
    
    xgb_model = xgb.train(params = params, dtrain = dtrain, num_boost_round = 400, evals = wlist)
    xgb_model_predict = xgb_model.predict(dtest)
    
    fpr, tpr, thresholds = metrics.roc_curve(y_test, xgb_model_predict)
    precision, recall, thresholds = precision_recall_curve(y_test, xgb_model_predict)
    
    f1_scores = 2*recall*precision/(recall+precision)
    
    
    _dict = {
        'max_depth' : max_depth,
        'best threshold' : thresholds[np.argmax(f1_scores)],
        'best F1-score' : np.max(f1_scores),
        'auc' : np.trapz(tpr, fpr)
    }

    grid.append(_dict)
 
 pd.DataFrame(grid)
 
 # eta = 0.05, num_boost_round = 1000
 
 grid = []

for max_depth in [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]:    
    params = {'max_depth' : max_depth,
             'eta' : 0.05, 
             'objective' : 'binary:logistic',
             'eval_metric' : 'logloss',
             'early_stoppings' : 50 }
    
    xgb_model = xgb.train(params = params, dtrain = dtrain, num_boost_round = 1000, evals = wlist)
    xgb_model_predict = xgb_model.predict(dtest)
    
    fpr, tpr, thresholds = metrics.roc_curve(y_test, xgb_model_predict)
    precision, recall, thresholds = precision_recall_curve(y_test, xgb_model_predict)
    f1_scores = 2*recall*precision/(recall+precision)
    
    
    _dict = {
        'max_depth' : max_depth,
        'best threshold' : thresholds[np.argmax(f1_scores)],
        'best F1-score' : np.max(f1_scores),
        'auc' : np.trapz(tpr, fpr)
    }

    grid.append(_dict)
    
 pd.DataFrame(grid)
 
 # eta = 0.1, num_boost_round = 1000
 
 grid = []

for max_depth in [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]:    
    params = {'max_depth' : max_depth,
             'eta' : 0.1, 
             'objective' : 'binary:logistic',
             'eval_metric' : 'logloss',
             'early_stoppings' : 50 }
    
    xgb_model = xgb.train(params = params, dtrain = dtrain, num_boost_round = 1000, evals = wlist)
    xgb_model_predict = xgb_model.predict(dtest)
    
    fpr, tpr, thresholds = metrics.roc_curve(y_test, xgb_model_predict)
    precision, recall, thresholds = precision_recall_curve(y_test, xgb_model_predict)
    f1_scores = 2*recall*precision/(recall+precision)
    
    
    _dict = {
        'max_depth' : max_depth,
        'best threshold' : thresholds[np.argmax(f1_scores)],
        'best F1-score' : np.max(f1_scores),
        'auc' : np.trapz(tpr, fpr)
    }

    grid.append(_dict)
    
 pd.DataFrame(grid)
 
 # eta = 0.15, num_boost_round = 1000
 
 grid = []

for max_depth in [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]:    
    params = {'max_depth' : max_depth,
             'eta' : 0.15, 
             'objective' : 'binary:logistic',
             'eval_metric' : 'logloss',
             'early_stoppings' : 50 }
    
    xgb_model = xgb.train(params = params, dtrain = dtrain, num_boost_round = 1000, evals = wlist)
    xgb_model_predict = xgb_model.predict(dtest)
    
    fpr, tpr, thresholds = metrics.roc_curve(y_test, xgb_model_predict)
    precision, recall, thresholds = precision_recall_curve(y_test, xgb_model_predict)
    f1_scores = 2*recall*precision/(recall+precision)
    
    
    _dict = {
        'max_depth' : max_depth,
        'best threshold' : thresholds[np.argmax(f1_scores)],
        'best F1-score' : np.max(f1_scores),
        'auc' : np.trapz(tpr, fpr)
    }

    grid.append(_dict)
    
pd.DataFrame(grid)

# eta = 0.2, num_boost_round = 1000

grid = []

for max_depth in [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]:    
    params = {'max_depth' : max_depth,
             'eta' : 0.2, 
             'objective' : 'binary:logistic',
             'eval_metric' : 'logloss',
             'early_stoppings' : 50 }
    
    xgb_model = xgb.train(params = params, dtrain = dtrain, num_boost_round = 1000, evals = wlist)
    xgb_model_predict = xgb_model.predict(dtest)
    
    fpr, tpr, thresholds = metrics.roc_curve(y_test, xgb_model_predict)
    precision, recall, thresholds = precision_recall_curve(y_test, xgb_model_predict)
    
    f1_scores = 2*recall*precision/(recall+precision)
    
    
    _dict = {
        'max_depth' : max_depth,
        'best threshold' : thresholds[np.argmax(f1_scores)],
        'best F1-score' : np.max(f1_scores),
        'auc' : np.trapz(tpr, fpr)
    }

    grid.append(_dict)
    
pd.DataFrame(grid)

#max_depth = 7 이 무난해 보임. 
~~~


##### k_fold cross validation
> 13_9_K-Fold Cross Validation.ipynb
~~~python
import pandas as pd
import numpy as np

from sklearn.model_selection import train_test_split
from sklearn import metrics
from sklearn.metrics import confusion_matrix
from sklearn.metrics import accuracy_score, roc_auc_score, roc_curve, precision_recall_curve

import matplotlib.pyplot as plt

# 개별 feature PCA 한 데이터 가져오기

x_scaled = pd.read_csv('x_scaled_with_pca.csv가 저장되어 있는 경로', encoding = 'cp949')

# target 가져오기

model_data = pd.read_csv('model_data.csv가 저장되어 있는 경로', encoding = 'cp949', thousands = ',')

model_data.drop(['corp_code', 'corp_name'], axis = 1, inplace = True)
y_data = model_data['도산']

## Stratified K-Fold CV
from sklearn.model_selection import StratifiedKFold
from imblearn.over_sampling import SMOTE
from sklearn.ensemble import VotingClassifier
from sklearn.linear_model import LogisticRegression
from sklearn import svm
from sklearn import tree
from sklearn.neighbors import KNeighborsClassifier

import xgboost as xgb

from sklearn.ensemble import RandomForestClassifier

smote = SMOTE(sampling_strategy = 1, k_neighbors = 5)

# 10-Fold CV

cv = StratifiedKFold(n_splits = 10)

SVM = []
Voting = []
Random_Forest = []
XGBoost_1 = []
XGBoost_2 = []

for train_idx, test_idx in cv.split(x_scaled, y_data):
    
    # K-Fold 분할
    x_train, y_train = x_scaled.iloc[train_idx], y_data[train_idx]
    x_test, y_test = x_scaled.iloc[test_idx], y_data[test_idx]
    
    
    # 분할된 train set에 smote로 증강
    x_train_r, y_train_r = smote.fit_resample(x_train, y_train)

    
    
    ## 1. SVM : 개별 분류기 중 가장 강력했던 모형
    # 기존 최적화했던 하이퍼 파라미터 적용
    
    
    svm_clf = svm.SVC(kernel = 'rbf', C = 1, probability = True)
    
    svm_clf.fit(x_train_r, y_train_r)
    y_pred = svm_clf.predict_proba(x_test)[: , 1]
    
    fpr, tpr, thresholds = metrics.roc_curve(y_test, y_pred)
    precision, recall, thresholds = precision_recall_curve(y_test, y_pred)
    
    f1_scores = 2*recall*precision/(recall+precision)
    
    _dict = {
        'best threshold' : thresholds[np.argmax(f1_scores)],
        'best F1-score' : np.max(f1_scores),
        'auc' : np.trapz(tpr, fpr)
    }
    
    SVM.append(_dict)
    
    
    ## 2. Voting
    # 기존 최적화했던 하이퍼 파라미터 적용

    lr_clf = LogisticRegression()
    svm_clf = svm.SVC(kernel = 'rbf', C = 1, probability = True)
    dt_clf = tree.DecisionTreeClassifier(max_depth = 6)
    knn_clf = KNeighborsClassifier(35)
    
    
    svot_clf = VotingClassifier(estimators = [('Logistic', lr_clf), ('SVM', svm_clf), ('DT', dt_clf), ('kNN', knn_clf)],
                                voting = 'soft')
    
    
    svot_clf.fit(x_train_r, y_train_r)
    y_pred = svot_clf.predict_proba(x_test)[: , 1]
    
    fpr, tpr, thresholds = metrics.roc_curve(y_test, y_pred)
    precision, recall, thresholds = precision_recall_curve(y_test, y_pred)
    
    f1_scores = 2*recall*precision/(recall+precision)
    
    _dict = {
        'best threshold' : thresholds[np.argmax(f1_scores)],
        'best F1-score' : np.max(f1_scores),
        'auc' : np.trapz(tpr, fpr)
    }
    
    Voting.append(_dict)
    
    
    
    ## 3. Random Forest
    # 기존 최적화했던 하이퍼 파라미터 적용
    
    rf_clf = RandomForestClassifier(n_estimators = 1000,
                                    max_depth = 20,
                                    max_features = 'auto',
                                    n_jobs = -1,
                                    verbose = 1)
    
    
    rf_clf.fit(x_train_r, y_train_r)
    y_pred = rf_clf.predict_proba(x_test)[: , 1]
    
    fpr, tpr, thresholds = metrics.roc_curve(y_test, y_pred)
    precision, recall, thresholds = precision_recall_curve(y_test, y_pred)
    
    f1_scores = 2*recall*precision/(recall+precision)
    
    _dict = {
        'best threshold' : thresholds[np.argmax(f1_scores)],
        'best F1-score' : np.max(f1_scores),
        'auc' : np.trapz(tpr, fpr)
    }
    
    Random_Forest.append(_dict)
    
    
    ## 4. XGBoost - 1
    # 기존 최적화했던 하이퍼 파라미터 적용
    
    dtrain = xgb.DMatrix(data = x_train_r, label = y_train_r)
    dtest = xgb.DMatrix(data = x_test, label = y_test)
    
    params = {'max_depth' : 7,
             'eta' : 0.15, 
             'objective' : 'binary:logistic',
             'eval_metric' : 'logloss',
             'early_stoppings' : 50 }
    
    wlist = [(dtrain, 'train'), (dtest, 'eval')]
    
    xgb_model = xgb.train(params = params, dtrain = dtrain, num_boost_round = 500, evals = wlist)
    
    y_pred = xgb_model.predict(dtest)
    
    fpr, tpr, thresholds = metrics.roc_curve(y_test, y_pred)
    precision, recall, thresholds = precision_recall_curve(y_test, y_pred)
    
    f1_scores = 2*recall*precision/(recall+precision)
    
    _dict = {
        'best threshold' : thresholds[np.argmax(f1_scores)],
        'best F1-score' : np.max(f1_scores),
        'auc' : np.trapz(tpr, fpr)
    }
    
    XGBoost_1.append(_dict)
    
    
    ## 5. XGBoost - 2
    # 기존 최적화했던 하이퍼 파라미터 적용
    
    dtrain = xgb.DMatrix(data = x_train_r, label = y_train_r)
    dtest = xgb.DMatrix(data = x_test, label = y_test)
    
    params = {'max_depth' : 7,
             'eta' : 0.15, 
             'objective' : 'binary:logistic',
             'eval_metric' : 'logloss',
             'early_stoppings' : 50 }
    
    wlist = [(dtrain, 'train'), (dtest, 'eval')]
    
    xgb_model = xgb.train(params = params, dtrain = dtrain, num_boost_round = 1000, evals = wlist)
    
    y_pred = xgb_model.predict(dtest)
    
    fpr, tpr, thresholds = metrics.roc_curve(y_test, y_pred)
    precision, recall, thresholds = precision_recall_curve(y_test, y_pred)
    
    f1_scores = 2*recall*precision/(recall+precision)
    
    _dict = {
        'best threshold' : thresholds[np.argmax(f1_scores)],
        'best F1-score' : np.max(f1_scores),
        'auc' : np.trapz(tpr, fpr)
    }
    
    XGBoost_2.append(_dict)
    
df_SVM = pd.DataFrame(SVM)
df_Voting = pd.DataFrame(Voting)
df_Random_Forest = pd.DataFrame(Random_Forest)
df_XGBoost_1 = pd.DataFrame(XGBoost_1)
df_XGBoost_2 = pd.DataFrame(XGBoost_2)

dict_SVM = {
    'mean_AUC' : df_SVM['auc'].mean(),
    'mean_Best_threshold' : df_SVM['best threshold'].mean(),
    'mean_Best_F1_score' : df_SVM['best F1-score'].mean()
}

dict_Voting = {
    'mean_AUC' : df_Voting['auc'].mean(),
    'mean_Best_threshold' : df_Voting['best threshold'].mean(),
    'mean_Best_F1_score' : df_Voting['best F1-score'].mean()
}

dict_Random_Forest = {
    'mean_AUC' : df_Random_Forest['auc'].mean(),
    'mean_Best_threshold' : df_Random_Forest['best threshold'].mean(),
    'mean_Best_F1_score' : df_Random_Forest['best F1-score'].mean()
}

dict_XGBoost_1 = {
    'mean_AUC' : df_XGBoost_1['auc'].mean(),
    'mean_Best_threshold' : df_XGBoost_1['best threshold'].mean(),
    'mean_Best_F1_score' : df_XGBoost_1['best F1-score'].mean()
}

dict_XGBoost_2 = {
    'mean_AUC' : df_XGBoost_2['auc'].mean(),
    'mean_Best_threshold' : df_XGBoost_2['best threshold'].mean(),
    'mean_Best_F1_score' : df_XGBoost_2['best F1-score'].mean()
}

Table = [dict_SVM, dict_Voting, dict_Random_Forest, dict_XGBoost_1, dict_XGBoost_2]
df_Table = pd.DataFrame(Table)
df_Table.index = ['SVM', 'Voting', 'Random_Forest', 'XGBoost_1', 'XGBoost_2']

df_Table.to_csv('K-Fold Cross Validation with 5 candidate models.csv', encoding = 'cp949')
~~~
#### 재무 feature 모델링
##### 재무 feature만 가져오기
> 14_1 재무 feature만 가져오기.ipynb
~~~python
import pandas as pd
x_scaled = pd.read_csv('x_scaled_with_pca.csv가 저장되어 있는 경로', encoding = 'cp949')
fin_scaled = x_scaled.drop(['1인당 월 평균 납부하는 국민연금 금액', 'SBHI', '연간 이직율', '존속연수', '접근성 PC1'], axis = 1)
fin_scaled.to_csv('fin_scaled.csv', encoding = 'cp949', index = False)
~~~
##### 로지스틱 모델링_재무
> 14_2_로지스틱 모델링.ipynb
~~~python
import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
from sklearn import metrics
from sklearn.metrics import confusion_matrix
from sklearn.metrics import accuracy_score, roc_auc_score, roc_curve, precision_recall_curve

import matplotlib.pyplot as plt

# 재무비율 데이터 가져오기

x_scaled = pd.read_csv('fin_scaled.csv가 저장되어 있는 경로', encoding = 'cp949')

# target 가져오기

model_data = pd.read_csv('model_data.csv가 저장되어 있는 경로', encoding = 'cp949', thousands = ',')

model_data.drop(['corp_code', 'corp_name'], axis = 1, inplace = True)
y_data = model_data['도산']

# 훈련-시험 데이터 분할

x_train, x_test, y_train, y_test = train_test_split(x_scaled, y_data, 
                                                     train_size = 0.8,
                                                     stratify = y_data)
# 데이터 증강
from sklearn.datasets import make_classification
from imblearn.over_sampling import SMOTE

smote = SMOTE(sampling_strategy = 1, k_neighbors = 5)
x_train_r, y_train_r = smote.fit_resample(x_train, y_train)

lr_clf = LogisticRegression(max_iter = 1000)
lr_clf.fit(x_train_r, y_train_r)
y_pred = lr_clf.predict_proba(x_test)[:, 1]

# ROC Curve

fpr, tpr, thresholds = metrics.roc_curve(y_test, y_pred)

plt.plot(fpr, tpr)

auc = np.trapz(tpr, fpr)
print('AUC : ', auc)

precision, recall, thresholds = precision_recall_curve(y_test, y_pred)

f1_scores = 2*recall*precision/(recall+precision)
print('Best threshold: ', thresholds[np.argmax(f1_scores)])
print('Best F1-Score: ', np.max(f1_scores))

# statsmodel로 summary 보기
import statsmodels.api as sm
model = sm.Logit(y_train_r, x_train_r)

results = model.fit(method = 'newton')
results.summary()
~~~

##### svm_재무
> 14_3_SVM.ipynb
~~~python
import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn import metrics
from sklearn.metrics import confusion_matrix
from sklearn.metrics import accuracy_score, roc_auc_score, roc_curve, precision_recall_curve

import matplotlib.pyplot as plt

# 개별 feature PCA 한 데이터 가져오기

x_scaled = pd.read_csv('x_scaled_with_pca.csv이 ', encoding = 'cp949')

# target 가져오기

model_data = pd.read_csv('model_data.csv가 저장되어 있는 경로', encoding = 'cp949', thousands = ',')

model_data.drop(['corp_code', 'corp_name'], axis = 1, inplace = True)
y_data = model_data['도산']

# 훈련-시험 데이터 분할
x_train, x_test, y_train, y_test = train_test_split(x_scaled, y_data, 
                                                     train_size = 0.8,
                                                     stratify = y_data)
# 데이터 증강

from sklearn.datasets import make_classification
from imblearn.over_sampling import SMOTE

smote = SMOTE(sampling_strategy = 1, k_neighbors = 5)
x_train_r, y_train_r = smote.fit_resample(x_train, y_train)

# kernel, C 조정하면서 roc curve, f1-score 보기
from sklearn import svm

# kernel = rbf, C = 0.05
clf = svm.SVC(kernel = 'rbf', C = 0.05, probability = True)
clf.fit(x_train_r, y_train_r)
y_pred = clf.predict_proba(x_test)[: , 1]

# ROC Curve

fpr, tpr, thresholds = metrics.roc_curve(y_test, y_pred)

plt.plot(fpr, tpr)

auc = np.trapz(tpr, fpr)
print('AUC : ', auc)

precision, recall, thresholds = precision_recall_curve(y_test, y_pred)

f1_scores = 2*recall*precision/(recall+precision)
print('Best threshold: ', thresholds[np.argmax(f1_scores)])
print('Best F1-Score: ', np.max(f1_scores))

# kernel = linear, C = 0.05
clf = svm.SVC(kernel = 'linear', C = 0.05, probability = True)
clf.fit(x_train_r, y_train_r)
y_pred = clf.predict_proba(x_test)[: , 1]


# ROC Curve

fpr, tpr, thresholds = metrics.roc_curve(y_test, y_pred)

plt.plot(fpr, tpr)

auc = np.trapz(tpr, fpr)
print('AUC : ', auc)

precision, recall, thresholds = precision_recall_curve(y_test, y_pred)

f1_scores = 2*recall*precision/(recall+precision)
print('Best threshold: ', thresholds[np.argmax(f1_scores)])
print('Best F1-Score: ', np.max(f1_scores))

# kernel = rbf, C = 0.1
clf = svm.SVC(kernel = 'rbf', C = 0.1, probability = True)
clf.fit(x_train_r, y_train_r)
y_pred = clf.predict_proba(x_test)[: , 1]

# ROC Curve

fpr, tpr, thresholds = metrics.roc_curve(y_test, y_pred)

plt.plot(fpr, tpr)

auc = np.trapz(tpr, fpr)
print('AUC : ', auc)

precision, recall, thresholds = precision_recall_curve(y_test, y_pred)

f1_scores = 2*recall*precision/(recall+precision)
print('Best threshold: ', thresholds[np.argmax(f1_scores)])
print('Best F1-Score: ', np.max(f1_scores))

# kernel = rbf, C = 0.5
clf = svm.SVC(kernel = 'rbf', C = 0.5, probability = True)
clf.fit(x_train_r, y_train_r)
y_pred = clf.predict_proba(x_test)[: , 1]

# ROC Curve

fpr, tpr, thresholds = metrics.roc_curve(y_test, y_pred)

plt.plot(fpr, tpr)

auc = np.trapz(tpr, fpr)
print('AUC : ', auc)

precision, recall, thresholds = precision_recall_curve(y_test, y_pred)

f1_scores = 2*recall*precision/(recall+precision)
print('Best threshold: ', thresholds[np.argmax(f1_scores)])
print('Best F1-Score: ', np.max(f1_scores))

# kernel = rbf, C = 1
clf = svm.SVC(kernel = 'rbf', C = 1, probability = True)
clf.fit(x_train_r, y_train_r)
y_pred = clf.predict_proba(x_test)[: , 1]

# ROC Curve

fpr, tpr, thresholds = metrics.roc_curve(y_test, y_pred)

plt.plot(fpr, tpr)

auc = np.trapz(tpr, fpr)
print('AUC : ', auc)

precision, recall, thresholds = precision_recall_curve(y_test, y_pred)

f1_scores = 2*recall*precision/(recall+precision)
print('Best threshold: ', thresholds[np.argmax(f1_scores)])
print('Best F1-Score: ', np.max(f1_scores))

# kernel = rbf, C = 5
clf = svm.SVC(kernel = 'rbf', C = 5, probability = True)
clf.fit(x_train_r, y_train_r)
y_pred = clf.predict_proba(x_test)[: , 1]

# ROC Curve

fpr, tpr, thresholds = metrics.roc_curve(y_test, y_pred)

plt.plot(fpr, tpr)

auc = np.trapz(tpr, fpr)
print('AUC : ', auc)

precision, recall, thresholds = precision_recall_curve(y_test, y_pred)

f1_scores = 2*recall*precision/(recall+precision)
print('Best threshold: ', thresholds[np.argmax(f1_scores)])
print('Best F1-Score: ', np.max(f1_scores))

# kernel = rbf, C = 10
clf = svm.SVC(kernel = 'rbf', C = 10, probability = True)
clf.fit(x_train_r, y_train_r)
y_pred = clf.predict_proba(x_test)[: , 1]

# ROC Curve

fpr, tpr, thresholds = metrics.roc_curve(y_test, y_pred)

plt.plot(fpr, tpr)

auc = np.trapz(tpr, fpr)
print('AUC : ', auc)

precision, recall, thresholds = precision_recall_curve(y_test, y_pred)

f1_scores = 2*recall*precision/(recall+precision)
print('Best threshold: ', thresholds[np.argmax(f1_scores)])
print('Best F1-Score: ', np.max(f1_scores))

# kernel = rbf, C = 1 결정
~~~

##### 의사결정트리_재무
> 14_4_Decision Tree.ipynb
~~~python
import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn import metrics
from sklearn.metrics import confusion_matrix
from sklearn.metrics import accuracy_score, roc_auc_score, roc_curve, precision_recall_curve

import matplotlib.pyplot as plt

# 재무비율 데이터 가져오기

x_scaled = pd.read_csv('fin_scaled.csv가 저장되어 있는 경로', encoding = 'cp949')

# target 가져오기

model_data = pd.read_csv('model_data.csv가 저장되어 있는 ', encoding = 'cp949', thousands = ',')

model_data.drop(['corp_code', 'corp_name'], axis = 1, inplace = True)
y_data = model_data['도산']

# 훈련-시험 데이터 분할
x_train, x_test, y_train, y_test = train_test_split(x_scaled, y_data, 
                                                     train_size = 0.8,
                                                     stratify = y_data)
# 데이터 증강                                                     
from sklearn.datasets import make_classification
from imblearn.over_sampling import SMOTE

smote = SMOTE(sampling_strategy = 1, k_neighbors = 5)
x_train_r, y_train_r = smote.fit_resample(x_train, y_train)


# max_depth 조절하면서 roc curve, f1-score 보기
from sklearn import tree
score = []

for i in range(3, 20):
    clf = tree.DecisionTreeClassifier(max_depth = i)
    clf.fit(x_train_r, y_train_r)
    
    y_pred = clf.predict_proba(x_test)[:, 1]
    
    fpr, tpr, thresholds = metrics.roc_curve(y_test, y_pred)
    precision, recall, thresholds = precision_recall_curve(y_test, y_pred)
    
    auc = np.trapz(tpr, fpr)
    
    f1_scores = 2*recall*precision/(recall+precision)
    
    best_threshold = thresholds[np.argmax(f1_scores)]
    best_f1_score = np.max(f1_scores)
    
    _dict = {
        'auc' : auc,
        'best_threshold' : best_threshold,
        'best_f1_score' : best_f1_score
    }
    
    score.append(_dict)
df_score = pd.DataFrame(score)
df_score.index = range(3, 20)

plt.plot(df_score['auc'])
plt.plot(df_score['best_f1_score'])

# 여러번 시행했을 때, max_depth = 6 정도가 적절해 보임
~~~

##### knn_재무
> 14_5_kNN.ipynb
~~~python
import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn import metrics
from sklearn.metrics import confusion_matrix
from sklearn.metrics import accuracy_score, roc_auc_score, roc_curve, precision_recall_curve

import matplotlib.pyplot as plt

# 재무비율 데이터 가져오기

x_scaled = pd.read_csv('fin_scaled.csv가 저장되어 있는 경로', encoding = 'cp949')

# target 가져오기

model_data = pd.read_csv('model_data.csv가 저장되어 있는 경로', encoding = 'cp949', thousands = ',')

model_data.drop(['corp_code', 'corp_name'], axis = 1, inplace = True)
y_data = model_data['도산']

# 훈련-시험 데이터 분할
x_train, x_test, y_train, y_test = train_test_split(x_scaled, y_data, 
                                                     train_size = 0.8,
                                                     stratify = y_data)
# 데이터 증강
from sklearn.datasets import make_classification
from imblearn.over_sampling import SMOTE

smote = SMOTE(sampling_strategy = 1, k_neighbors = 5)
x_train_r, y_train_r = smote.fit_resample(x_train, y_train)

from sklearn.neighbors import KNeighborsClassifier
# n_neighbors 조절하면서 auc, f1-score 보기

score = []

for i in range(1, 100):
    clf = KNeighborsClassifier(i)
    clf.fit(x_train_r, y_train_r)
    
    y_pred = clf.predict_proba(x_test)[:, 1]
    
    fpr, tpr, thresholds = metrics.roc_curve(y_test, y_pred)
    precision, recall, thresholds = precision_recall_curve(y_test, y_pred)
    
    auc = np.trapz(tpr, fpr)
    
    f1_scores = 2*recall*precision/(recall+precision)
    
    best_threshold = thresholds[np.argmax(f1_scores)]
    best_f1_score = np.max(f1_scores)
    
    _dict = {
        'auc' : auc,
        'best_threshold' : best_threshold,
        'best_f1_score' : best_f1_score
    }
    
    score.append(_dict)
    
df_score = pd.DataFrame(score)
df_score.index = range(1, 100)

plt.plot(df_score['auc'])
plt.plot(df_score['best_f1_score'])
# n_neighbors = 55 정도로 결정
~~~

##### 앙상블_보팅_재무
> 14_6_Ensemble Method_Voting.ipynb
~~~python
import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn import metrics
from sklearn.metrics import confusion_matrix
from sklearn.metrics import accuracy_score, roc_auc_score, roc_curve, precision_recall_curve


import matplotlib.pyplot as plt

# 재무비율 데이터 가져오기

x_scaled = pd.read_csv('fin_scaled.csv가 저장되어 있는 경로', encoding = 'cp949')

# target 가져오기

model_data = pd.read_csv('model_data.csv가 저장되어 있는 경로', encoding = 'cp949', thousands = ',')

model_data.drop(['corp_code', 'corp_name'], axis = 1, inplace = True)

y_data = model_data['도산']

# 훈련-시험 데이터 분할

x_train, x_test, y_train, y_test = train_test_split(x_scaled, y_data, 
                                                     train_size = 0.8,
                                                     stratify = y_data)



# 데이터 증강

from sklearn.datasets import make_classification
from imblearn.over_sampling import SMOTE

smote = SMOTE(sampling_strategy = 1, k_neighbors = 5)

x_train_r, y_train_r = smote.fit_resample(x_train, y_train)



## 1. 보팅 앙상블 기법 적용

from sklearn.ensemble import VotingClassifier
from sklearn.linear_model import LogisticRegression
from sklearn import svm
from sklearn import tree
from sklearn.neighbors import KNeighborsClassifier

# 기존 최적화했던 하이퍼 파라미터 적용

lr_clf = LogisticRegression()
svm_clf = svm.SVC(kernel = 'rbf', C = 1, probability = True)
dt_clf = tree.DecisionTreeClassifier(max_depth = 6)
knn_clf = KNeighborsClassifier(n_neighbors = 55)



# 소프트 보팅

svot_clf = VotingClassifier(estimators = [('Logistic', lr_clf), ('SVM', svm_clf), ('DT', dt_clf), ('kNN', knn_clf)],
                            voting = 'soft')

svot_clf.fit(x_train_r, y_train_r)

svot_clf_pred = svot_clf.predict(x_test)


print(accuracy_score(y_test, svot_clf_pred))



# threshold 조절해서 ROC curve 그려보기

y_pred = svot_clf.predict_proba(x_test)[: , 1]

# ROC Curve :

fpr, tpr, thresholds = metrics.roc_curve(y_test, y_pred)

plt.plot(fpr, tpr)

auc = np.trapz(tpr, fpr)
print('AUC : ', auc)



# f1_score의 최댓값과 그 때의 threshold 찾기

precision, recall, thresholds = precision_recall_curve(y_test, y_pred)

f1_scores = 2*recall*precision/(recall+precision)
print('Best threshold: ', thresholds[np.argmax(f1_scores)])
print('Best F1-Score: ', np.max(f1_scores))
~~~


##### 앙상블_랜덤 포레스트_재무
> 14_7_Ensemble Method_Random Forest.ipynb
~~~python
import pandas as pd
import numpy as np

from sklearn.model_selection import train_test_split
from sklearn import metrics
from sklearn.metrics import confusion_matrix
from sklearn.metrics import accuracy_score, roc_auc_score, roc_curve, precision_recall_curve

import matplotlib.pyplot as plt



# 재무비율 데이터 가져오기

x_scaled = pd.read_csv('fin_scaled.csv가 저장되어 있는 경로', encoding = 'cp949')

x_scaled

# target 가져오기

model_data = pd.read_csv('model_data.csv가 저장되어 있는 경로', encoding = 'cp949', thousands = ',')

model_data.drop(['corp_code', 'corp_name'], axis = 1, inplace = True)

y_data = model_data['도산']

# 훈련-시험 데이터 분할

x_train, x_test, y_train, y_test = train_test_split(x_scaled, y_data, 
                                                     train_size = 0.8,
                                                     stratify = y_data)



# 데이터 증강

from sklearn.datasets import make_classification
from imblearn.over_sampling import SMOTE

smote = SMOTE(sampling_strategy = 1, k_neighbors = 5)

x_train_r, y_train_r = smote.fit_resample(x_train, y_train)



from sklearn.ensemble import RandomForestClassifier

# max_depth 조절하면서 auc, f1-score 보기

score = []

for i in range(5, 40):
    rf_clf = RandomForestClassifier(n_estimators = 1000,
                                    max_depth = i,
                                    max_features = 'auto',
                                    verbose = 1,
                                    n_jobs = -1)
    
    rf_clf.fit(x_train_r, y_train_r)
    y_pred = rf_clf.predict_proba(x_test)[: , 1]
    
    fpr, tpr, thresholds = metrics.roc_curve(y_test, y_pred)
    precision, recall, thresholds = precision_recall_curve(y_test, y_pred)
    
    auc = np.trapz(tpr, fpr)
    
    f1_scores = 2*recall*precision/(recall+precision)
    
    best_threshold = thresholds[np.argmax(f1_scores)]
    best_f1_score = np.max(f1_scores)
    
    _dict = {
        'auc' : auc,
        'best_threshold' : best_threshold,
        'best_f1_score' : best_f1_score
    }
    
    score.append(_dict)



df_score = pd.DataFrame(score)

df_score.index = range(5, 40)

# df_score



plt.plot(df_score['auc'])

plt.plot(df_score['best_f1_score'])

## 25개 이상 정도면 적당한 것 같음



rf_clf = RandomForestClassifier(n_estimators = 1000,
                                    max_depth = 25,
                                    max_features = 'auto',
                                    verbose = 1,
                                    n_jobs = -1)
    
rf_clf.fit(x_train_r, y_train_r)



def plot_feature_importance(model):
    n_features = x_scaled.shape[1]
    plt.barh(np.arange(n_features), sorted(model.feature_importances_), align="center")
    plt.yticks(np.arange(n_features), x_scaled.columns)
    plt.xlabel("Random Forest Feature Importance")
    plt.ylabel("Feature")
    plt.ylim(-1, n_features)

plt.rc('font', family = 'Malgun Gothic')

plot_feature_importance(rf_clf)
~~~

##### 앙상블_xgboost_재무
> 14_8_Ensemble Method_XGBoost.ipynb
~~~python
import pandas as pd
import numpy as np

from sklearn.model_selection import train_test_split
from sklearn import metrics
from sklearn.metrics import confusion_matrix
from sklearn.metrics import accuracy_score, roc_auc_score, roc_curve, precision_recall_curve

import matplotlib.pyplot as plt



# 재무비율 데이터 가져오기

x_scaled = pd.read_csv('fin_scaled.csv가 저장되어 있는 경로', encoding = 'cp949')

# x_scaled

# target 가져오기

model_data = pd.read_csv('model_data.csv가 저장되어 있는 경로', encoding = 'cp949', thousands = ',')

model_data.drop(['corp_code', 'corp_name'], axis = 1, inplace = True)

y_data = model_data['도산']

# 훈련-시험 데이터 분할

x_train, x_test, y_train, y_test = train_test_split(x_scaled, y_data, 
                                                     train_size = 0.8,
                                                     stratify = y_data)



# 데이터 증강

from sklearn.datasets import make_classification
from imblearn.over_sampling import SMOTE

smote = SMOTE(sampling_strategy = 1, k_neighbors = 5)

x_train_r, y_train_r = smote.fit_resample(x_train, y_train)



import xgboost as xgb
from xgboost import plot_importance

# DMatrix 변환

dtrain = xgb.DMatrix(data = x_train_r, label = y_train_r)
dtest = xgb.DMatrix(data = x_test, label = y_test)

wlist = [(dtrain, 'train'), (dtest, 'eval')]



## max_depth, eta, num_boost_round 바꾸면서 f1-score, auc 보기 -> 대체적으로 7개가 적합해보임



# eta = 0.05, num_boost_round = 500

grid = []

for max_depth in [4, 5, 6, 7, 8, 9, 10, 11, 12, 13]:    
    params = {'max_depth' : max_depth,
             'eta' : 0.05, 
             'objective' : 'binary:logistic',
             'eval_metric' : 'logloss',
             'early_stoppings' : 50 }
    
    xgb_model = xgb.train(params = params, dtrain = dtrain, num_boost_round = 500, evals = wlist)
    xgb_model_predict = xgb_model.predict(dtest)
    
    fpr, tpr, thresholds = metrics.roc_curve(y_test, xgb_model_predict)
    precision, recall, thresholds = precision_recall_curve(y_test, xgb_model_predict)
    f1_scores = 2*recall*precision/(recall+precision)
    
    
    _dict = {
        'max_depth' : max_depth,
        'best threshold' : thresholds[np.argmax(f1_scores)],
        'best F1-score' : np.max(f1_scores),
        'auc' : np.trapz(tpr, fpr)
    }

    grid.append(_dict)

# pd.DataFrame(grid)



# eta = 0.1, num_boost_round = 500

grid = []

for max_depth in [4, 5, 6, 7, 8, 9, 10, 11, 12, 13]:    
    params = {'max_depth' : max_depth,
             'eta' : 0.1, 
             'objective' : 'binary:logistic',
             'eval_metric' : 'logloss',
             'early_stoppings' : 50 }
    
    xgb_model = xgb.train(params = params, dtrain = dtrain, num_boost_round = 500, evals = wlist)
    xgb_model_predict = xgb_model.predict(dtest)
    
    fpr, tpr, thresholds = metrics.roc_curve(y_test, xgb_model_predict)
    precision, recall, thresholds = precision_recall_curve(y_test, xgb_model_predict)
    f1_scores = 2*recall*precision/(recall+precision)
    
    
    _dict = {
        'max_depth' : max_depth,
        'best threshold' : thresholds[np.argmax(f1_scores)],
        'best F1-score' : np.max(f1_scores),
        'auc' : np.trapz(tpr, fpr)
    }

    grid.append(_dict)

# pd.DataFrame(grid)



# eta = 0.15, num_boost_round = 500

grid = []

for max_depth in [4, 5, 6, 7, 8, 9, 10, 11, 12, 13]:    
    params = {'max_depth' : max_depth,
             'eta' : 0.15, 
             'objective' : 'binary:logistic',
             'eval_metric' : 'logloss',
             'early_stoppings' : 50 }
    
    xgb_model = xgb.train(params = params, dtrain = dtrain, num_boost_round = 500, evals = wlist)
    xgb_model_predict = xgb_model.predict(dtest)
    
    fpr, tpr, thresholds = metrics.roc_curve(y_test, xgb_model_predict)
    precision, recall, thresholds = precision_recall_curve(y_test, xgb_model_predict)
    f1_scores = 2*recall*precision/(recall+precision)
    
    
    _dict = {
        'max_depth' : max_depth,
        'best threshold' : thresholds[np.argmax(f1_scores)],
        'best F1-score' : np.max(f1_scores),
        'auc' : np.trapz(tpr, fpr)
    }

    grid.append(_dict)

# pd.DataFrame(grid)



# eta = 0.2, num_boost_round = 500

grid = []

for max_depth in [4, 5, 6, 7, 8, 9, 10, 11, 12, 13]:    
    params = {'max_depth' : max_depth,
             'eta' : 0.2, 
             'objective' : 'binary:logistic',
             'eval_metric' : 'logloss',
             'early_stoppings' : 50 }
    
    xgb_model = xgb.train(params = params, dtrain = dtrain, num_boost_round = 500, evals = wlist)
    xgb_model_predict = xgb_model.predict(dtest)
    
    fpr, tpr, thresholds = metrics.roc_curve(y_test, xgb_model_predict)
    precision, recall, thresholds = precision_recall_curve(y_test, xgb_model_predict)
    f1_scores = 2*recall*precision/(recall+precision)
    
    
    _dict = {
        'max_depth' : max_depth,
        'best threshold' : thresholds[np.argmax(f1_scores)],
        'best F1-score' : np.max(f1_scores),
        'auc' : np.trapz(tpr, fpr)
    }

    grid.append(_dict)

# pd.DataFrame(grid)





# eta = 0.05, num_boost_round = 1000

grid = []

for max_depth in [4, 5, 6, 7, 8, 9, 10, 11, 12, 13]:    
    params = {'max_depth' : max_depth,
             'eta' : 0.05, 
             'objective' : 'binary:logistic',
             'eval_metric' : 'logloss',
             'early_stoppings' : 50 }
    
    xgb_model = xgb.train(params = params, dtrain = dtrain, num_boost_round = 1000, evals = wlist)
    xgb_model_predict = xgb_model.predict(dtest)
    
    fpr, tpr, thresholds = metrics.roc_curve(y_test, xgb_model_predict)
    precision, recall, thresholds = precision_recall_curve(y_test, xgb_model_predict)
    f1_scores = 2*recall*precision/(recall+precision)
    
    
    _dict = {
        'max_depth' : max_depth,
        'best threshold' : thresholds[np.argmax(f1_scores)],
        'best F1-score' : np.max(f1_scores),
        'auc' : np.trapz(tpr, fpr)
    }

    grid.append(_dict)

# pd.DataFrame(grid)



# eta = 0.1, num_boost_round = 1000

grid = []

for max_depth in [4, 5, 6, 7, 8, 9, 10, 11, 12, 13]:    
    params = {'max_depth' : max_depth,
             'eta' : 0.1, 
             'objective' : 'binary:logistic',
             'eval_metric' : 'logloss',
             'early_stoppings' : 50 }
    
    xgb_model = xgb.train(params = params, dtrain = dtrain, num_boost_round = 1000, evals = wlist)
    xgb_model_predict = xgb_model.predict(dtest)
    
    fpr, tpr, thresholds = metrics.roc_curve(y_test, xgb_model_predict)
    precision, recall, thresholds = precision_recall_curve(y_test, xgb_model_predict)
    f1_scores = 2*recall*precision/(recall+precision)
    
    
    _dict = {
        'max_depth' : max_depth,
        'best threshold' : thresholds[np.argmax(f1_scores)],
        'best F1-score' : np.max(f1_scores),
        'auc' : np.trapz(tpr, fpr)
    }

    grid.append(_dict)

# pd.DataFrame(grid)





# eta = 0.15, num_boost_round = 1000

grid = []

for max_depth in [4, 5, 6, 7, 8, 9, 10, 11, 12, 13]:    
    params = {'max_depth' : max_depth,
             'eta' : 0.15, 
             'objective' : 'binary:logistic',
             'eval_metric' : 'logloss',
             'early_stoppings' : 50 }
    
    xgb_model = xgb.train(params = params, dtrain = dtrain, num_boost_round = 1000, evals = wlist)
    xgb_model_predict = xgb_model.predict(dtest)
    
    fpr, tpr, thresholds = metrics.roc_curve(y_test, xgb_model_predict)
    precision, recall, thresholds = precision_recall_curve(y_test, xgb_model_predict)
    f1_scores = 2*recall*precision/(recall+precision)
    
    
    _dict = {
        'max_depth' : max_depth,
        'best threshold' : thresholds[np.argmax(f1_scores)],
        'best F1-score' : np.max(f1_scores),
        'auc' : np.trapz(tpr, fpr)
    }

    grid.append(_dict)

pd.DataFrame(grid)



# eta = 0.2, num_boost_round = 1000

grid = []

for max_depth in [4, 5, 6, 7, 8, 9, 10, 11, 12, 13]:    
    params = {'max_depth' : max_depth,
             'eta' : 0.2, 
             'objective' : 'binary:logistic',
             'eval_metric' : 'logloss',
             'early_stoppings' : 50 }
    
    xgb_model = xgb.train(params = params, dtrain = dtrain, num_boost_round = 1000, evals = wlist)
    xgb_model_predict = xgb_model.predict(dtest)
    
    fpr, tpr, thresholds = metrics.roc_curve(y_test, xgb_model_predict)
    precision, recall, thresholds = precision_recall_curve(y_test, xgb_model_predict)
    f1_scores = 2*recall*precision/(recall+precision)
    
    
    _dict = {
        'max_depth' : max_depth,
        'best threshold' : thresholds[np.argmax(f1_scores)],
        'best F1-score' : np.max(f1_scores),
        'auc' : np.trapz(tpr, fpr)
    }

    grid.append(_dict)

# pd.DataFrame(grid)





# eta = 0.05, num_boost_round = 250

grid = []

for max_depth in [4, 5, 6, 7, 8, 9, 10, 11, 12, 13]:    
    params = {'max_depth' : max_depth,
             'eta' : 0.05, 
             'objective' : 'binary:logistic',
             'eval_metric' : 'logloss',
             'early_stoppings' : 50 }
    
    xgb_model = xgb.train(params = params, dtrain = dtrain, num_boost_round = 250, evals = wlist)
    xgb_model_predict = xgb_model.predict(dtest)
    
    fpr, tpr, thresholds = metrics.roc_curve(y_test, xgb_model_predict)
    precision, recall, thresholds = precision_recall_curve(y_test, xgb_model_predict)
    f1_scores = 2*recall*precision/(recall+precision)
    
    
    _dict = {
        'max_depth' : max_depth,
        'best threshold' : thresholds[np.argmax(f1_scores)],
        'best F1-score' : np.max(f1_scores),
        'auc' : np.trapz(tpr, fpr)
    }

    grid.append(_dict)

# pd.DataFrame(grid)



# eta = 0.1, num_boost_round = 250

grid = []

for max_depth in [4, 5, 6, 7, 8, 9, 10, 11, 12, 13]:    
    params = {'max_depth' : max_depth,
             'eta' : 0.1, 
             'objective' : 'binary:logistic',
             'eval_metric' : 'logloss',
             'early_stoppings' : 50 }
    
    xgb_model = xgb.train(params = params, dtrain = dtrain, num_boost_round = 250, evals = wlist)
    xgb_model_predict = xgb_model.predict(dtest)
    
    fpr, tpr, thresholds = metrics.roc_curve(y_test, xgb_model_predict)
    precision, recall, thresholds = precision_recall_curve(y_test, xgb_model_predict)
    f1_scores = 2*recall*precision/(recall+precision)
    
    
    _dict = {
        'max_depth' : max_depth,
        'best threshold' : thresholds[np.argmax(f1_scores)],
        'best F1-score' : np.max(f1_scores),
        'auc' : np.trapz(tpr, fpr)
    }

    grid.append(_dict)

# pd.DataFrame(grid)



# eta = 0.15, num_boost_round = 250

grid = []

for max_depth in [4, 5, 6, 7, 8, 9, 10, 11, 12, 13]:    
    params = {'max_depth' : max_depth,
             'eta' : 0.15, 
             'objective' : 'binary:logistic',
             'eval_metric' : 'logloss',
             'early_stoppings' : 50 }
    
    xgb_model = xgb.train(params = params, dtrain = dtrain, num_boost_round = 250, evals = wlist)
    xgb_model_predict = xgb_model.predict(dtest)
    
    fpr, tpr, thresholds = metrics.roc_curve(y_test, xgb_model_predict)
    precision, recall, thresholds = precision_recall_curve(y_test, xgb_model_predict)
    f1_scores = 2*recall*precision/(recall+precision)
    
    
    _dict = {
        'max_depth' : max_depth,
        'best threshold' : thresholds[np.argmax(f1_scores)],
        'best F1-score' : np.max(f1_scores),
        'auc' : np.trapz(tpr, fpr)
    }

    grid.append(_dict)

# pd.DataFrame(grid)



# eta = 0.2, num_boost_round = 250

grid = []

for max_depth in [4, 5, 6, 7, 8, 9, 10, 11, 12, 13]:    
    params = {'max_depth' : max_depth,
             'eta' : 0.2, 
             'objective' : 'binary:logistic',
             'eval_metric' : 'logloss',
             'early_stoppings' : 50 }
    
    xgb_model = xgb.train(params = params, dtrain = dtrain, num_boost_round = 250, evals = wlist)
    xgb_model_predict = xgb_model.predict(dtest)
    
    fpr, tpr, thresholds = metrics.roc_curve(y_test, xgb_model_predict)
    precision, recall, thresholds = precision_recall_curve(y_test, xgb_model_predict)
    f1_scores = 2*recall*precision/(recall+precision)
    
    
    _dict = {
        'max_depth' : max_depth,
        'best threshold' : thresholds[np.argmax(f1_scores)],
        'best F1-score' : np.max(f1_scores),
        'auc' : np.trapz(tpr, fpr)
    }

    grid.append(_dict)

# pd.DataFrame(grid)



# max_depth = 7 이 괜찮아 보임
~~~

##### k_fold cross validation_재무
> 14_9_K-Fold Cross Validation.ipynb
~~~python
import pandas as pd
import numpy as np

from sklearn.model_selection import train_test_split
from sklearn import metrics
from sklearn.metrics import confusion_matrix
from sklearn.metrics import accuracy_score, roc_auc_score, roc_curve, precision_recall_curve

import matplotlib.pyplot as plt

# 재무비율 데이터 가져오기

x_scaled = pd.read_csv('fin_scaled.csv가 저장되어 있는 경로', encoding = 'cp949')

# target 가져오기

model_data = pd.read_csv('model_data.csv가 저장되어 있는 경로', encoding = 'cp949', thousands = ',')

model_data.drop(['corp_code', 'corp_name'], axis = 1, inplace = True)

y_data = model_data['도산']



## Stratified K-Fold CV

from sklearn.model_selection import StratifiedKFold
from imblearn.over_sampling import SMOTE

from sklearn.ensemble import VotingClassifier
from sklearn.linear_model import LogisticRegression
from sklearn import svm
from sklearn import tree
from sklearn.neighbors import KNeighborsClassifier

import xgboost as xgb

from sklearn.ensemble import RandomForestClassifier

smote = SMOTE(sampling_strategy = 1, k_neighbors = 5)

# 10-Fold CV

cv = StratifiedKFold(n_splits = 10)



SVM = []
Voting = []
Random_Forest = []
XGBoost_1 = []
XGBoost_2 = []

for train_idx, test_idx in cv.split(x_scaled, y_data):
    
    # K-Fold 분할
    x_train, y_train = x_scaled.iloc[train_idx], y_data[train_idx]
    x_test, y_test = x_scaled.iloc[test_idx], y_data[test_idx]
    
    
    # 분할된 train set에 smote로 증강
    x_train_r, y_train_r = smote.fit_resample(x_train, y_train)

    
    
    ## 1. SVM : 개별 분류기 중 가장 강력했던 모형
    # 기존 최적화했던 하이퍼 파라미터 적용
    
    
    svm_clf = svm.SVC(kernel = 'rbf', C = 1, probability = True)
    
    svm_clf.fit(x_train_r, y_train_r)
    y_pred = svm_clf.predict_proba(x_test)[: , 1]
    
    fpr, tpr, thresholds = metrics.roc_curve(y_test, y_pred)
    precision, recall, thresholds = precision_recall_curve(y_test, y_pred)
    
    f1_scores = 2*recall*precision/(recall+precision)
    
    _dict = {
        'best threshold' : thresholds[np.argmax(f1_scores)],
        'best F1-score' : np.max(f1_scores),
        'auc' : np.trapz(tpr, fpr)
    }
    
    SVM.append(_dict)
    
    
    ## 2. Voting
    # 기존 최적화했던 하이퍼 파라미터 적용

    lr_clf = LogisticRegression()
    svm_clf = svm.SVC(kernel = 'rbf', C = 1, probability = True)
    dt_clf = tree.DecisionTreeClassifier(max_depth = 6)
    knn_clf = KNeighborsClassifier(55)
    
    
    svot_clf = VotingClassifier(estimators = [('Logistic', lr_clf), ('SVM', svm_clf), ('DT', dt_clf), ('kNN', knn_clf)],
                                voting = 'soft')
    
    
    svot_clf.fit(x_train_r, y_train_r)
    y_pred = svot_clf.predict_proba(x_test)[: , 1]
    
    fpr, tpr, thresholds = metrics.roc_curve(y_test, y_pred)
    precision, recall, thresholds = precision_recall_curve(y_test, y_pred)
    
    f1_scores = 2*recall*precision/(recall+precision)
    
    _dict = {
        'best threshold' : thresholds[np.argmax(f1_scores)],
        'best F1-score' : np.max(f1_scores),
        'auc' : np.trapz(tpr, fpr)
    }
    
    Voting.append(_dict)
    
    
    
    ## 3. Random Forest
    # 기존 최적화했던 하이퍼 파라미터 적용
    
    rf_clf = RandomForestClassifier(n_estimators = 1000,
                                    max_depth = 25,
                                    max_features = 'auto',
                                    n_jobs = -1,
                                    verbose = 1)
    
    
    rf_clf.fit(x_train_r, y_train_r)
    y_pred = rf_clf.predict_proba(x_test)[: , 1]
    
    fpr, tpr, thresholds = metrics.roc_curve(y_test, y_pred)
    precision, recall, thresholds = precision_recall_curve(y_test, y_pred)
    
    f1_scores = 2*recall*precision/(recall+precision)
    
    _dict = {
        'best threshold' : thresholds[np.argmax(f1_scores)],
        'best F1-score' : np.max(f1_scores),
        'auc' : np.trapz(tpr, fpr)
    }
    
    Random_Forest.append(_dict)
    
    
    ## 4. XGBoost - 1
    # 기존 최적화했던 하이퍼 파라미터 적용
    
    dtrain = xgb.DMatrix(data = x_train_r, label = y_train_r)
    dtest = xgb.DMatrix(data = x_test, label = y_test)
    
    params = {'max_depth' : 7,
             'eta' : 0.1, 
             'objective' : 'binary:logistic',
             'eval_metric' : 'logloss',
             'early_stoppings' : 50 }
    
    wlist = [(dtrain, 'train'), (dtest, 'eval')]
    
    xgb_model = xgb.train(params = params, dtrain = dtrain, num_boost_round = 500, evals = wlist)
    
    y_pred = xgb_model.predict(dtest)
    
    fpr, tpr, thresholds = metrics.roc_curve(y_test, y_pred)
    precision, recall, thresholds = precision_recall_curve(y_test, y_pred)
    
    f1_scores = 2*recall*precision/(recall+precision)
    
    _dict = {
        'best threshold' : thresholds[np.argmax(f1_scores)],
        'best F1-score' : np.max(f1_scores),
        'auc' : np.trapz(tpr, fpr)
    }
    
    XGBoost_1.append(_dict)
    
    
    ## 5. XGBoost - 2
    # 기존 최적화했던 하이퍼 파라미터 적용
    
    dtrain = xgb.DMatrix(data = x_train_r, label = y_train_r)
    dtest = xgb.DMatrix(data = x_test, label = y_test)
    
    params = {'max_depth' : 7,
             'eta' : 0.1, 
             'objective' : 'binary:logistic',
             'eval_metric' : 'logloss',
             'early_stoppings' : 50 }
    
    wlist = [(dtrain, 'train'), (dtest, 'eval')]
    
    xgb_model = xgb.train(params = params, dtrain = dtrain, num_boost_round = 1000, evals = wlist)
    
    y_pred = xgb_model.predict(dtest)
    
    fpr, tpr, thresholds = metrics.roc_curve(y_test, y_pred)
    precision, recall, thresholds = precision_recall_curve(y_test, y_pred)
    
    f1_scores = 2*recall*precision/(recall+precision)
    
    _dict = {
        'best threshold' : thresholds[np.argmax(f1_scores)],
        'best F1-score' : np.max(f1_scores),
        'auc' : np.trapz(tpr, fpr)
    }
    
    XGBoost_2.append(_dict)

df_SVM = pd.DataFrame(SVM)
# df_SVM

df_Voting = pd.DataFrame(Voting)
# df_Voting

df_Random_Forest = pd.DataFrame(Random_Forest)
# df_Random_Forest

df_XGBoost_1 = pd.DataFrame(XGBoost_1)
# df_XGBoost_1

df_XGBoost_2 = pd.DataFrame(XGBoost_2)
# df_XGBoost_2



dict_SVM = {
    'mean_AUC' : df_SVM['auc'].mean(),
    'mean_Best_threshold' : df_SVM['best threshold'].mean(),
    'mean_Best_F1_score' : df_SVM['best F1-score'].mean()
}

dict_Voting = {
    'mean_AUC' : df_Voting['auc'].mean(),
    'mean_Best_threshold' : df_Voting['best threshold'].mean(),
    'mean_Best_F1_score' : df_Voting['best F1-score'].mean()
}

dict_Random_Forest = {
    'mean_AUC' : df_Random_Forest['auc'].mean(),
    'mean_Best_threshold' : df_Random_Forest['best threshold'].mean(),
    'mean_Best_F1_score' : df_Random_Forest['best F1-score'].mean()
}

dict_XGBoost_1 = {
    'mean_AUC' : df_XGBoost_1['auc'].mean(),
    'mean_Best_threshold' : df_XGBoost_1['best threshold'].mean(),
    'mean_Best_F1_score' : df_XGBoost_1['best F1-score'].mean()
}

dict_XGBoost_2 = {
    'mean_AUC' : df_XGBoost_2['auc'].mean(),
    'mean_Best_threshold' : df_XGBoost_2['best threshold'].mean(),
    'mean_Best_F1_score' : df_XGBoost_2['best F1-score'].mean()
}



Table = [dict_SVM, dict_Voting, dict_Random_Forest, dict_XGBoost_1, dict_XGBoost_2]

df_Table = pd.DataFrame(Table)

# df_Table

df_Table.index = ['SVM', 'Voting', 'Random_Forest', 'XGBoost_1', 'XGBoost_2']

# df_Table



df_Table.to_csv('K-Fold Cross Validation with 5 candidate models.csv', encoding = 'cp949')
~~~

## 시각화
#### 법정동코드 가져오기
> 15_0_주소로 법정동코드 가져오기.ipynb
1. 최종 데이터 'final_data_3.csv'의 주소와 법정동코드 파일 'sig_cd.csv'를 결합하여 법정동코드를 가져옴
> 결과 데이터 : 'final_data_4.csv'
~~~python
import requests
import pandas as pd
import numpy as np

final_data = pd.read_csv('final_data_3(주소 수정).csv가 저장되어 있는 경로', encoding = 'cp949')

list_final_data_address = final_data['상세주소']




sig_cd_data = pd.read_csv('sig_cd.csv가 저장되어 있는 경로', encoding = 'cp949')

sig_cd_data['기타'] = sig_cd_data['기타'].fillna('')

sig_cd_data['시도'] = sig_cd_data['시도'].fillna('')

list_sig_cd_data_address = sig_cd_data['시도'] + ' ' + sig_cd_data['시군구'] + ' ' + sig_cd_data['기타']

list_index = list_sig_cd_data_address.index

sig_cd_data = pd.concat([sig_cd_data['SIG_CD'], list_sig_cd_data_address], axis = 1)

sig_cd_data.columns = ['SIG_CD', 'address']

sig_cd_data['address'][0].split()

list_sig_cd = []

for final_data_address in list_final_data_address:
    
    for index, sig_cd_data_address in zip(list_index, list_sig_cd_data_address):
        
        if final_data_address.split()[0:3] == sig_cd_data_address.split():
            sig_cd = sig_cd_data['SIG_CD'][index]
            break
            
        elif final_data_address.split()[0:2] == sig_cd_data_address.split():
            sig_cd = sig_cd_data['SIG_CD'][index]
            break
            
        else:
            sig_cd = None
        
    list_sig_cd.append(sig_cd)

df_sig_cd = pd.DataFrame(list_sig_cd)

df_sig_cd.columns = ['sig_cd']

final_data = pd.concat([final_data, df_sig_cd], axis = 1)

final_data.to_csv('final_data_4.csv', encoding = 'cp949', index = False)
~~~

#### 좌표계 위치데이터 시각화
> 15_1_좌표계 위치데이터 시각화.ipynb
1. 접근성 지표에 해당하는 '주변 편의점 개수' 와 '정류장 개수'의 지역별 평균을 시각화
~~~python
import folium
from folium import plugins

import pandas as pd
import json

kr_geo_path = 'TL_SCCO_SIG.json가 저장되어 있는 경로'
kr_geo = json.load(open(kr_geo_path, encoding = 'utf-8'))
center = [36.57, 127.87]

m = folium.Map(location = center, zoom_start = 7.2)
folium.GeoJson(kr_geo).add_to(m)

final_data = pd.read_csv('final_data_4.csv가 저장되어 있는 경로', encoding = 'cp949')

location_count_df = final_data.groupby('sig_cd').agg({'sig_cd' : 'count', '주변 편의점 개수' : 'sum', '정류장 개수' : 'sum', '연간 이직율' : 'sum', '1인당 월 평균 납부하는 국민연금 금액' : 'sum'})

location_count_df.columns = ['count', 'sum of stores', 'sum of stations', 'sum of turnover', 'sum of nps']

location_count_df = location_count_df.reset_index()

location_count_df['sig_cd'] = location_count_df['sig_cd'].astype(int).astype(str)

location_count_df['mean of stores'] = location_count_df['sum of stores'] / location_count_df['count']
location_count_df['mean of stations'] = location_count_df['sum of stations'] / location_count_df['count']
location_count_df['mean of turnover'] = location_count_df['sum of turnover'] / location_count_df['count']
location_count_df['mean of nps'] = location_count_df['sum of nps'] / location_count_df['count']

m = folium.Map(location = center, zoom_start = 7.5, tiles = None)

folium.Choropleth(geo_data = kr_geo, name = 'Stores',
                 data = location_count_df, columns = ['sig_cd', 'mean of stores'],
                 key_on = 'feature.properties.SIG_CD',
                 fill_color='YlOrRd', fill_opacity = 0.8, line_opacity = 0.2,
                  nan_fill_opacity = 0.5, legend_name = 'Frequency of Stores').add_to(m)

m = folium.Map(location = center, zoom_start = 7.2, tiles = None)

folium.Choropleth(geo_data = kr_geo, name = 'Stations',
                 data = location_count_df, columns = ['sig_cd', 'mean of stations'],
                 key_on = 'feature.properties.SIG_CD',
                 fill_color='YlOrRd', fill_opacity = 0.6, line_opacity = 0.2, legend_name = 'Frequency of Stations').add_to(m)

# 이직률은 크게 관계없는듯?

m = folium.Map(location = center, zoom_start = 7.2, tiles = None)

folium.Choropleth(geo_data = kr_geo, name = 'Stations',
                 data = location_count_df, columns = ['sig_cd', 'mean of turnover'],
                 key_on = 'feature.properties.SIG_CD',
                 fill_color='YlOrRd', fill_opacity = 0.6, line_opacity = 0.2, legend_name = 'turnover rate').add_to(m)

# 국민연금 납부 금액도.. 몇몇 공단 지역 제외하고는 눈에 띄는 인사이트가 안 보임 (포항, 울산, 창원, 여수, 광양, 군산, 서산)

m = folium.Map(location = center, zoom_start = 7.2, tiles = None)

folium.Choropleth(geo_data = kr_geo, name = 'Stations',
                 data = location_count_df, columns = ['sig_cd', 'mean of nps'],
                 key_on = 'feature.properties.SIG_CD',
                 fill_color='YlOrRd', fill_opacity = 0.6, line_opacity = 0.2, legend_name = 'mean of nps').add_to(m)
~~~

#### 비재무적 지표 파이그래프 및 feature 보정 전후 비교
> 15_2_남은 비재무적 지표 파이그래프 & feature 보정 전후 비교.ipynb
1. '연간이직율'과 '기업 존속연수' 파이그래프 시각화
2. feature 보정 전후를 비교하기 쉽게, 모든 변수들의 보정 전 후 히스토그램 혹은 커널 밀도 시각화
~~~python
import pandas as pd
import numpy as np

### model_data의 모든 분포는 재스코어링한 분포로, 실제 분포가 아님 ###
### PPT 반영시 주의할 것. 데이터 전처리 과정에 포함해야 할 것 같음 ###

# 최종 변수 final_data

final_data = pd.read_csv('final_data_3.csv가 저장되어 있는 경로', encoding = 'cp949', thousands = ',')

# 변수 재스코어링한 model_data

model_data = pd.read_csv('model_data.csv가 저장되어 있는 경로', encoding = 'cp949')

model_data = model_data.drop(['corp_code', 'corp_name'], axis = 1)



import matplotlib.pyplot as plt
import matplotlib
import seaborn as sns

plt.rc('font', family = 'Malgun Gothic')
matplotlib.rcParams['axes.unicode_minus'] = False

# 1. SBHI : 경공업 / 중화학공업 / 건설업 / 도소매업 / 기타   5개 범주로 크게 나누어서 수직선으로 표현해도 좋을듯
# 2. 연간 이직율 : 0~50%, 50~100%, 100~200%, 200%~ 비율로 파이 그래프 or 비율 막대 그래프 그려도 좋을듯
# 3. 존속연수 : 0~10년, 10~20년, 20~30년, 30년~ 비율로 파이 그래프 or 비율 막대 그래프 그려도 좋을듯

# 1. 은 파워포인트에서 해야 하나...?

# 2.

# 연간 이직율별 카테고리부터 만들기

def make_turnover_cat(x):
    if (x > 0) & (x < 50):
        return ' ~ 50%'
    
    elif (x >= 50) & (x < 100):
        return '50% ~ 100%'
    
    elif (x >= 100) & (x < 200):
        return '100% ~ 200%'
    
    else:
        return '200% ~'

final_data['turnover_cat'] = final_data['연간 이직율'].apply(make_turnover_cat)


# 연간 이직율 파이차트 만들기

frequency = final_data.groupby(['turnover_cat'])['turnover_cat'].count()


labels = [' ~ 50%', '50% ~ 100%', '100% ~ 200%', '200% ~']


fig = plt.figure(figsize=(8,8))
ax = fig.add_subplot()

pie = ax.pie(frequency, ## 파이차트 출력
             colors = sns.color_palette('hls',len(labels)),
             startangle=90, ## 시작점을 90도(degree)로 지정
             counterclock=False, ## 시계 방향으로 그린다.
             wedgeprops=dict(width = 0.3) ## 중간의 반지름 0.5만큼 구멍을 뚫어준다.
            )


total = np.sum(frequency) ## 빈도수 총합
 
sum_pct = 0 ## 백분율 초기값

for i,l in enumerate(labels):
    ang1, ang2 = pie[0][i].theta1, pie[0][i].theta2 ## 각1, 각2
    r = pie[0][i].r ## 원의 반지름
    
    x = ((r+0.7)/2)*np.cos(np.pi/180*((ang1+ang2)/2)) ## 정중앙 x좌표
    y = ((r+0.7)/2)*np.sin(np.pi/180*((ang1+ang2)/2)) ## 정중앙 y좌표
    
    if i < len(labels) - 1:
        sum_pct += float(f'{frequency[i]/total*100:.2f}') ## 백분율을 누적한다.
        ax.text(x,y,f'{frequency[i]/total*100:.2f}%',ha='center',va='center') ## 백분율 텍스트 표시
    else: ## 총합을 100으로 맞추기위해 마지막 백분율은 100에서 백분율 누적값을 빼준다.
        ax.text(x,y,f'{100-sum_pct:.2f}%',ha='center',va='center')
        
plt.legend(labels)

plt.show()



# 3.

# 존속연수 카테고리부터 만들기

def make_survival_cat(x):
    if (x > 0) & (x < 10):
        return ' ~ 10년'
    
    elif (x >= 10) & (x < 20):
        return '10년 ~ 20년'
    
    elif (x >= 20) & (x < 30):
        return '20년 ~ 30년'
    
    else:
        return '30년 ~'

final_data['survival_cat'] = final_data['존속연수'].apply(make_survival_cat)


frequency = final_data.groupby(['survival_cat'])['survival_cat'].count()

labels = [' ~ 10년', '10년 ~ 20년', '20년 ~ 30년', '30년 ~']

fig = plt.figure(figsize=(8,8))
ax = fig.add_subplot()

pie = ax.pie(frequency, ## 파이차트 출력
             colors = sns.color_palette('hls',len(labels)),
             startangle=90, ## 시작점을 90도(degree)로 지정
             counterclock=False, ## 시계 방향으로 그린다.
             wedgeprops=dict(width = 0.3) ## 중간의 반지름 0.5만큼 구멍을 뚫어준다.
            )


total = np.sum(frequency) ## 빈도수 총합
 
sum_pct = 0 ## 백분율 초기값

for i,l in enumerate(labels):
    ang1, ang2 = pie[0][i].theta1, pie[0][i].theta2 ## 각1, 각2
    r = pie[0][i].r ## 원의 반지름
    
    x = ((r+0.7)/2)*np.cos(np.pi/180*((ang1+ang2)/2)) ## 정중앙 x좌표
    y = ((r+0.7)/2)*np.sin(np.pi/180*((ang1+ang2)/2)) ## 정중앙 y좌표
    
    if i < len(labels) - 1:
        sum_pct += float(f'{frequency[i]/total*100:.2f}') ## 백분율을 누적한다.
        ax.text(x,y,f'{frequency[i]/total*100:.2f}%',ha='center',va='center') ## 백분율 텍스트 표시
    else: ## 총합을 100으로 맞추기위해 마지막 백분율은 100에서 백분율 누적값을 빼준다.
        ax.text(x,y,f'{100-sum_pct:.2f}%',ha='center',va='center')
        
plt.legend(labels)

plt.show()

### 이제 히스토그램과 KDE 보기 ###

# 원래 feature

# 1인당 월 평균 납부하는 국민연금 금액

sns.histplot(data = final_data, x = model_data.columns[0], bins = 30, kde = True)
plt.show()

# SBHI

sns.histplot(data = final_data, x = model_data.columns[1], bins = 10, kde = True)
plt.show()

# 주변 편의점 개수

sns.histplot(data = final_data, x = model_data.columns[2], bins = 20, kde = True)
plt.show()

# 정류장 개수

sns.histplot(data = final_data, x = model_data.columns[3], bins = 20, kde = True)
plt.show()

# 연간 이직율

sns.histplot(data = final_data, x = model_data.columns[4], bins = 30, kde = True)
plt.show()

# 존속연수

sns.histplot(data = final_data, x = model_data.columns[5], bins = 15, kde = True)
plt.show()

# 순이익률
# 이하 모든 재무비율은 극단값 때문에 모두 이런 형태를 띔 -> 보정치와 비교할 것

sns.kdeplot(data = final_data, x = model_data.columns[6], shade = True)
plt.show()

# 영업이익률

sns.kdeplot(data = final_data, x = model_data.columns[7], shade = True)
plt.show()

# 매출총이익률

sns.kdeplot(data = final_data, x = model_data.columns[8], shade = True)
plt.show()

# 총자산순이익률

sns.kdeplot(data = final_data, x = model_data.columns[9], shade = True)
plt.show()

# 자본금이익률

sns.kdeplot(data = final_data, x = model_data.columns[10], shade = True)
plt.show()

# 매출액증가율

sns.kdeplot(data = final_data, x = model_data.columns[11], shade = True)
plt.show()

# 영업이익증가율

sns.kdeplot(data = final_data, x = model_data.columns[12], shade = True)
plt.show()

# 순이익증가율

sns.kdeplot(data = final_data, x = model_data.columns[13], shade = True)
plt.show()

# 총자본회전율

sns.kdeplot(data = final_data, x = model_data.columns[14], shade = True)
plt.show()

# 자기자본회전율

sns.kdeplot(data = final_data, x = model_data.columns[15], shade = True)
plt.show()

# 유동성비율

sns.kdeplot(data = final_data, x = model_data.columns[16], shade = True)
plt.show()

# 당좌비율

sns.kdeplot(data = final_data, x = model_data.columns[17], shade = True)
plt.show()

# 부채비율

sns.kdeplot(data = final_data, x = model_data.columns[18], shade = True)
plt.show()



# 보정한 feature

# 1인당 월 평균 납부하는 국민연금 금액

sns.histplot(data = model_data, x = model_data.columns[0], bins = 30, kde = True)
plt.show()

# SBHI

sns.histplot(data = model_data, x = model_data.columns[1], bins = 10, kde = True)
plt.show()

# 주변 편의점 개수

sns.histplot(data = model_data, x = model_data.columns[2], bins = 15, kde = True)
plt.show()

# 정류장 개수

sns.histplot(data = model_data, x = model_data.columns[3], bins = 15, kde = True)
plt.show()

# 연간 이직율

sns.histplot(data = model_data, x = model_data.columns[4], bins = 20, kde = True)
plt.show()

# 존속연수

sns.histplot(data = model_data, x = model_data.columns[5], bins = 15, kde = True)
plt.show()

# 순이익률

sns.kdeplot(data = model_data, x = model_data.columns[6], shade = True)
plt.show()

# 영업이익률

sns.kdeplot(data = model_data, x = model_data.columns[7], shade = True)
plt.show()

# 매출총이익률

sns.kdeplot(data = model_data, x = model_data.columns[8], shade = True)
plt.show()

# 총자산순이익률

sns.kdeplot(data = model_data, x = model_data.columns[9], shade = True)
plt.show()

# 자본금이익률

sns.kdeplot(data = model_data, x = model_data.columns[10], shade = True)
plt.show()

# 매출액증가율

sns.kdeplot(data = model_data, x = model_data.columns[11], shade = True)
plt.show()

# 영업이익증가율

sns.kdeplot(data = model_data, x = model_data.columns[12], shade = True)
plt.show()

# 순이익증가율

sns.kdeplot(data = model_data, x = model_data.columns[13], shade = True)
plt.show()

# 총자본회전율

sns.kdeplot(data = model_data, x = model_data.columns[14], shade = True)
plt.show()

# 자기자본회전율

sns.kdeplot(data = model_data, x = model_data.columns[15], shade = True)
plt.show()

# 유동성비율

sns.kdeplot(data = model_data, x = model_data.columns[16], shade = True)
plt.show()

# 당좌비율

sns.kdeplot(data = model_data, x = model_data.columns[17], shade = True)
plt.show()

# 부채비율

sns.kdeplot(data = model_data, x = model_data.columns[18], shade = True)
plt.show()
~~~


## 테스트 데이터 전처리
#### 섹터별 sbhi 가져오기
> 16_0_섹터별 SBHI 가져오기.ipynb
1. 테스트 데이터 섹터별로 [KBIZ 중소기업중앙회](https://www.kbiz.or.kr/ko/index/index.do)의 SBHI 점수 입력
~~~python
import pandas as pd
import numpy as np

# 최종적으로 변수선택하여 전 지역 통합한 데이터

final_data = pd.read_csv('final_data_3.csv가 저장되어 있는 경로', encoding = 'cp949')

##### 2. 섹터에 따라 SBHI 입력하기 #####

list_sector = final_data['섹터']

# 각 섹터의 SBHI를 딕셔너리로 대응

sector_to_sbhi = {
    '농업, 임업 및 어업' : 72.5, # 비제조업
    '광업' : 72.5, # 비제조업
    '식료품' : 85.5,
    '음료' : 86.2,
    '섬유제품' : 73.4,
    '의복' : 73.1,
    '가죽 및 신발' : 59.9,
    '목재 및 나무제품' : 75.8,
    '인쇄 및 기록매체' : 70.5,
    '고무 및 플라스틱' : 73.3,
    '가구' : 71.3,
    '경공업 기타' : 76.4, # 경공업
    '펄프 및 종이' : 83.3,
    '화학제품' : 80.7,
    '의약품' : 96.6,
    '비금속광물' : 76.6,
    '1차금속' : 83.5,
    '금속가공' : 80.3,
    '전자부품, 컴퓨터, 영상음향' : 88.0,
    '의료, 정밀, 광학기기 및 시계' :84.2,
    '전기장비' : 78.8,
    '기계장비' : 82.5,
    '자동차 및 트레일러' : 87.1,
    '기타 운송장비' : 86.2,
    '중공업 기타' : 76.4, # 중공업
    '제조업 기타' : 80.7, # 제조업
    '전기, 가스, 증기 및 공기 조절 공급업' : 72.5, # 비제조업
    '수도, 하수 및 폐기물 처리, 원료 재생업' : 72.5, # 비제조업
    '건설업' : 75.2,
    '도매 및 소매업' : 72.1,
    '운수 및 창고업' : 72.7,
    '숙박 및 음식점업' : 53.4,
    '정보통신업' : 82.1,
    '금융 및 보험업' : 72.0, # 서비스업
    '부동산업' : 68.2,
    '전문, 과학 및 기술 서비스업' : 80.2,
    '공공 행정, 국방 및 사회보장 행정' : 72.0, # 서비스업
    '사업시설 관리, 사업 지원 및 임대 서비스업' : 72.8,
    '교육 서비스업' : 70.5,
    '보건업 및 사회복지 서비스업' : 72.0, # 서비스업
    '예술, 스포츠 및 여가관련 서비스업' : 69.5,
    '협회 및 단체, 수리 및 기타 개인 서비스업' : 66.6, 
    '가구 내 고용활동 및 달리 분류되지 않은 자가 소비 생산활동' : 75.3,  # 전산업
    '국제 및 외국기관' : 75.3,  # 전산업
    '기타' :75.3
}

list_sbhi = []

# 각 기업의 섹터에 대응되는 SBHI를 가져옴
for corp_code, corp_name, sector in zip(list_corp_code, list_corp_name, list_sector):
    
    try:
        sbhi = sector_to_sbhi[sector]
    except:
        sbhi = None
    
    each_sbhi = {
        'corp_code' : corp_code,
        'corp_name' : corp_name,
        'SBHI' : sbhi
    }
    
    list_sbhi.append(each_sbhi)

df_sbhi = pd.DataFrame(list_sbhi)

final_data['SBHI'] = df_sbhi['SBHI']

final_data.to_csv('final_data_3.csv', encoding = 'cp949', index = False)
~~~

#### 테스트 데이터 수치변환 및 feature 선정
> 16_0_수치변환하고 feature만 남기기.ipynb
~~~python
import pandas as pd
import numpy as np

final_data = pd.read_csv('final_data_3.csv가 저장되어 있는 경로', encoding = 'cp949', thousands = ',')

model_data = final_data[['corp_code', 'corp_name']]

# 1. 1인당 월 평균 납부하는 국민연금 금액, SBHI
# 그대로 입력

final_data.iloc[:, [9, 27]]

model_data =  pd.concat([model_data, final_data.iloc[:, [9, 27]]], axis = 1)

# 2. 주변 편의점 개수, 정류장 개수, 연간 이직율, 존속연수
# 루트 처리

final_data.iloc[:, [7, 8, 10, 11]]

def sqrt_revision(x):
    if x < 0:
        x = -np.sqrt(abs(x))
    
    else:
        x = np.sqrt(x)
    
    return(x)

for num in [7, 8, 10, 11]:
    model_data = pd.concat([model_data, final_data.iloc[:, num].apply(sqrt_revision)], axis = 1)

# 3. 부채비율을 제외한 재무비율
# 양수의 경우 : 해당 값과 제 99 분위수 중 작은 값의 루트값
# 음수의 경우 : 해당 값과 제 1 분위수 중 큰 값의 절댓값의 루트값의 음수

def sqrt_revision(x):
    if x < 0:
        x = -np.sqrt(abs(max(x, lower_quantile)))
    
    else:
        x = np.sqrt(min(x, upper_quantile))
    
    return(x)

for num in [12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 23, 24]:
    
    upper_quantile = final_data.iloc[:, num].quantile(0.99)
    lower_quantile = final_data.iloc[:, num].quantile(0.01)
    
    model_data = pd.concat([model_data, final_data.iloc[:, num].apply(sqrt_revision)], axis = 1)

# 4. 부채비율
# 양수의 경우 해당 값과 제 99 분위수 중 작은 값의 루트값
# 음수의 경우 제 99 분위수의 루트값

def sqrt_limit_revision(x):
    if x <= 0:
        x = np.sqrt(upper_quantile)
    
    else:
        x = np.sqrt(min(x, upper_quantile))
    
    return(x)

upper_quantile = final_data.iloc[:, 22].quantile(0.99)

final_data.iloc[:, 22].apply(sqrt_limit_revision)

model_data = pd.concat([model_data, final_data.iloc[:, 22].apply(sqrt_limit_revision)], axis = 1)

test_data = model_data

test_data.to_csv('test_data.csv', encoding = 'cp949', index = False)
~~~

#### 테스트 데이터 표준화 및 개별 pca
> 16_1_2021년 데이터 표준화, 개별 PCA.ipynb
~~~python
import pandas as pd
import numpy as np

test_data = pd.read_csv('test_data.csv가 저장되어 있는 경로', encoding = 'cp949', thousands = ',')

test_data.drop(['corp_code', 'corp_name'], axis = 1, inplace = True)

# test_data.info()



## 1. 데이터 표준화

from sklearn.preprocessing import RobustScaler

scaler = RobustScaler()

test_scaled = pd.DataFrame(scaler.fit_transform(test_data))

test_scaled.columns = test_data.columns

test_scaled.to_csv('test_scaled.csv', encoding = 'cp949', index = False)

from sklearn.decomposition import PCA

# 1. 주변 편의점 개수 & 정류장 개수

data_1 = test_scaled[['주변 편의점 개수', '정류장 개수']]

pca = PCA(n_components = 2)

pc_1 = pca.fit_transform(data_1)

df_pc_1 = pd.DataFrame(data = pc_1)

df_pc_1 = df_pc_1.iloc[:, 0]

df_pc_1 = pd.DataFrame(df_pc_1)

df_pc_1.columns = ['접근성 PC1']

# 2. 순이익률, 영업이익률, 매출총이익률, 총자산이익률, 자본금이익률

data_2 = test_scaled[['순이익률', '영업이익률', '매출총이익률', '총자산순이익률(ROA)', '자본금이익률(ROE)']]

pca = PCA(n_components = 5)

pc_2 = pca.fit_transform(data_2)

df_pc_2 = pd.DataFrame(data = pc_2)

df_pc_2 = df_pc_2.iloc[:, 0:2]

df_pc_2.columns = ['수익성 PC1', '수익성 PC2']

# 3. 영업이익증가율, 순이익증가율

data_3 = test_scaled[['영업이익증가율', '순이익증가율']]

pca = PCA(n_components = 2)

pc_3 = pca.fit_transform(data_3)

df_pc_3 = pd.DataFrame(data = pc_3)

df_pc_3 = df_pc_3.iloc[:, 0]

df_pc_3 = pd.DataFrame(df_pc_3)

df_pc_3.columns = ['이익증가율 PC1']

# 4. 총자본회전율, 자기자본회전율

data_4 = test_scaled[['총자본회전율', '자기자본회전율']]

pca = PCA(n_components = 2)

pc_4 = pca.fit_transform(data_4)

df_pc_4 = pd.DataFrame(data = pc_4)

df_pc_4 = df_pc_4.iloc[:, 0]

df_pc_4 = pd.DataFrame(df_pc_4)

df_pc_4.columns = ['활동성 PC1']

# 5. 유동성비율, 당좌비율

data_5 = test_scaled[['유동성비율', '당좌비율']]

pca = PCA(n_components = 2)

pc_5 = pca.fit_transform(data_5)

df_pc_5 = pd.DataFrame(data = pc_5)

df_pc_5 = df_pc_5.iloc[:, 0]
df_pc_5 = pd.DataFrame(df_pc_5)

df_pc_5.columns = ['안정성 PC1']

test_scaled = test_scaled.drop(['주변 편의점 개수', '정류장 개수', '순이익률', '영업이익률', '매출총이익률', '총자산순이익률(ROA)', '자본금이익률(ROE)', '영업이익증가율', '순이익증가율', '총자본회전율', '자기자본회전율', '유동성비율', '당좌비율'], axis = 1)

test_scaled = pd.concat([test_scaled, df_pc_1, df_pc_2, df_pc_3, df_pc_4, df_pc_5], axis = 1)

test_scaled.to_csv('test_scaled_with_pca.csv', encoding = 'cp949', index = False)
~~~

## 모델 테스트

#### 테스트 데이터 활용 모델 테스트
> 16_2_2021년 데이터 예측
~~~python
import pandas as pd
import numpy as np

from sklearn.model_selection import train_test_split
from sklearn import metrics
from sklearn.metrics import confusion_matrix
from sklearn.metrics import accuracy_score, roc_auc_score, roc_curve, precision_recall_curve

import matplotlib.pyplot as plt

# 2020년 개별 feature PCA + 스케일링 한 데이터 가져오기

x_scaled = pd.read_csv('x_scaled_with_pca.csv가 저장되어 있는 경로', encoding = 'cp949')

# target 가져오기

model_data = pd.read_csv('model_data.csv가 저장되어 있는 경로', encoding = 'cp949', thousands = ',')

model_data.drop(['corp_code', 'corp_name'], axis = 1, inplace = True)

y_data = model_data['도산']



# 2020년 재무 데이터만

fin_scaled = x_scaled.drop(['1인당 월 평균 납부하는 국민연금 금액', 'SBHI', '연간 이직율', '존속연수', '접근성 PC1'], axis = 1)

# 2021년 개별 feature PCA + 스케일링 한 데이터 가져오기

test_scaled = pd.read_csv('test_scaled_with_pca.csv가 저장되어 있는 경로', encoding = 'cp949')

# test_scaled.info()

# 2021년 재무 데이터만

fin_test_scaled = test_scaled.drop(['1인당 월 평균 납부하는 국민연금 금액', 'SBHI', '연간 이직율', '존속연수', '접근성 PC1'], axis = 1)

from sklearn.ensemble import RandomForestClassifier

## 1. 재무 + 비재무 결합 모형

# 2020년 데이터로 모형 학습

rf_clf = RandomForestClassifier(n_estimators = 1000,
                                    max_depth = 20,
                                    max_features = 'auto',
                                    verbose = 1,
                                    n_jobs = -1)
    
rf_clf.fit(x_scaled, y_data)


# 2021년 데이터 예측

combined_pred = rf_clf.predict_proba(test_scaled)[:, 1]


## 2. 재무 단일 모형

rf_clf = RandomForestClassifier(n_estimators = 1000,
                                    max_depth = 25,
                                    max_features = 'auto',
                                    verbose = 1,
                                    n_jobs = -1)
    
rf_clf.fit(fin_scaled, y_data)

fin_pred = rf_clf.predict_proba(fin_test_scaled)[:, 1]


# 원본 feature가 들어 있는 2021년 final_data_3에 붙여넣기

final_data = pd.read_csv('final_data_3.csv가 저장되어 있는 경로', encoding = 'cp949')
final_data['combined_pred'] = combined_pred
final_data['fin_pred'] = fin_pred
final_data['difference'] = final_data['combined_pred'] - final_data['fin_pred']
final_data.to_csv('final_data_with_difference.csv', encoding = 'cp949', index = False)
~~~

#### 예측결과 비교
> 16_3_예측결과 비교.ipynb
~~~python
import pandas as pd

test_data = pd.read_csv('final_data_with_difference.csv가 저장되어 있는 경로', encoding = 'cp949')

test_data['difference']

# 도산 예측확률이 결합 모형에서 재무 모형대비 5%p 이상 상승

pos_dif = test_data['difference'] > 0.05

# 도산 예측확률이 결합 모형에서 재무 모형대비 5%p 이상 하락

neg_dif = test_data['difference'] < -0.05

from scipy import stats

# SBHI

t_stat, p_val_1 = stats.ttest_ind(test_data.loc[pos_dif]['SBHI'], test_data.loc[neg_dif]['SBHI'], equal_var = True, alternative = 'two-sided')

# 주변 편의점 개수

t_stat, p_val_2 = stats.ttest_ind(test_data.loc[pos_dif]['주변 편의점 개수'], test_data.loc[neg_dif]['주변 편의점 개수'], equal_var = True, alternative = 'two-sided')

# 정류장 개수

t_stat, p_val_3 = stats.ttest_ind(test_data.loc[pos_dif]['정류장 개수'], test_data.loc[neg_dif]['정류장 개수'], equal_var = True, alternative = 'two-sided')

# 연간 이직률

t_stat, p_val_4 = stats.ttest_ind(test_data.loc[pos_dif]['연간 이직율'], test_data.loc[neg_dif]['연간 이직율'], equal_var = True, alternative = 'two-sided')

# 국민연금 납부금액

t_stat, p_val_5 = stats.ttest_ind(test_data.loc[pos_dif]['1인당 월 평균 납부하는 국민연금 금액'], test_data.loc[neg_dif]['1인당 월 평균 납부하는 국민연금 금액'], equal_var = True, alternative = 'two-sided')

Pos = {
    'SBHI' : round(test_data.loc[pos_dif]['SBHI'].mean(), 3),
    '주변 편의점 개수' : round(test_data.loc[pos_dif]['주변 편의점 개수'].mean(), 3),
    '정류장 개수' : round(test_data.loc[pos_dif]['정류장 개수'].mean(), 3),
    '연간 이직율' : round(test_data.loc[pos_dif]['연간 이직율'].mean(), 3),
    '1인당 월 평균 납부하는 국민연금 금액' : round(test_data.loc[pos_dif]['1인당 월 평균 납부하는 국민연금 금액'].mean())
}

Neg = {
    'SBHI' : round(test_data.loc[neg_dif]['SBHI'].mean(), 3),
    '주변 편의점 개수' : round(test_data.loc[neg_dif]['주변 편의점 개수'].mean(), 3),
    '정류장 개수' : round(test_data.loc[neg_dif]['정류장 개수'].mean(), 3),
    '연간 이직율' : round(test_data.loc[neg_dif]['연간 이직율'].mean(), 3),
    '1인당 월 평균 납부하는 국민연금 금액' : round(test_data.loc[neg_dif]['1인당 월 평균 납부하는 국민연금 금액'].mean())
}

t_test = {
    'SBHI' : round(p_val_1, 3),
    '주변 편의점 개수' : round(p_val_2, 3),
    '정류장 개수' : round(p_val_3, 3),
    '연간 이직율' : round(p_val_4, 3),
    '1인당 월 평균 납부하는 국민연금 금액' : round(p_val_5, 3)
}

list_mean = [Pos, Neg, t_test]

df_mean = pd.DataFrame(list_mean)

df_mean.index = ['대조모형 대비 5%p 이상 상승', '대조모형 대비 5%p 이상 하락', 't-test']

df_mean
~~~
