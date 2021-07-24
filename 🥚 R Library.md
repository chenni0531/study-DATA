# 🥚 R library

[TOC]

### `dplyr`

- 데이터프레임 처리에 특화된 패키지

- 파이프라인(`%>%`) 연산자 사용
  - 최소한의 변수만 지정하여 데이터 핸들링 가능
  - 코드의 가독성 증가

**컬럼 이름 바꾸기**

```r
rename(데이터프레임, 바꾼 후의 열 이름1 = 바뀌기 전 열 이름1, ...) 
데이터프레임 %>% rename(바꾼 후의 열 이름1 = 바뀌기 전 열 이름1, ...)
```

**새로운 컬럼 만들기**

```r
데이터프레임 %>% mutate(열 이름1 = 열 내용1,
                 열 이름2 = 열 내용2, ...)
```

**필요한 행만 추출하기**

```r
데이터프레임 %>% filter(조건)
```

**필요한 컬럼만 추출하기**

```r
데이터프레임 %>% select(열 이름1, 열 이름2, ...)
```

**순서대로 정렬하기**

```r
데이터프레임 %>% arrange(열 이름)
```

**컬럼 별 요약하기**

```r
데이터프레임 %>% group_by(열 이름) %>% summarise()
emp%>%
  group_by(DEPARTMENT_ID)%>%
  summarise(sum_sal = sum(SALARY), mean_sal = mean(SALARY))
```

**집단 별 요약하기**

```r
데이터프레임 %>% summarise(열 이름 = 요약정보)
emp%>%
  summarise(sum_sal = sum(SALARY), mean_sal = mean(SALARY))
```

```r
# summarise_at 특정한 열에 대해 원하는 그룹함수 여러 개를 한 번에 사용 가능
emp%>%
  summarise_at(c('SALARY','COMMISSION_PCT'),
                      c(sum, mean), na.rm=T)
```

```r
# summarise_if 해당되는 데이터에 모두 함수 적용
emp%>%
  summarise_if(is.numeric,sum)
```

**파이프라인은 중첩 가능**

```r
emp%>%
  filter(SALARY> 
           max(emp%>%
           filter(JOB_ID=='SA_REP')%>%
           select(SALARY))
         )%>%
  select(LAST_NAME,SALARY,JOB_ID) 
```

