# Cover-letter-automate
It is a project to automate raw cover letters without polishing

Requires more time to improve structure and gramma.

```{r setup, include=FALSE}
library(dplyr)
knitr::opts_chunk$set(echo = FALSE, warning = FALSE, message = FALSE, include = FALSE)
```

```{r import}
library(glue)
path <- "D:/My Storage/Career_R_ABS/cover letter/"
comp_detail <- readxl::read_xlsx(paste0(path,"Company details.xlsx"))
```


::: from
**Wenwei Fei**     
Clayton, VIC 3168  
Email: wenwei.fei@outlook.com  
linkedin: [wenwei-fei-tim](https://www.linkedin.com/in/wenwei-fei-tim/)  
Phone: 0416898866  
github: [github.com/wwfeitim](https://github.com/wwfeitim)  
Blog: [timminilab.blogspot](https://timminilab.blogspot.com/)  
:::

```{r date}
date <- Sys.Date() %>% format(., "%b %d %Y")
```

::: date
`r paste(date)`
:::

```{r company row}
rownumber <- 10
```

```{r company details}
manager_name <- comp_detail[rownumber,][,"HR_Name"] %>% unlist() %>% ifelse(is.na(.) == "TRUE","Hiring Manager", .)
company_name <- comp_detail[rownumber,][,"Company_Name"] %>% unlist() %>% ifelse(is.na(.) == "TRUE","No company name?", .)
company_address <- comp_detail[rownumber,][,"Address"] %>% unlist() %>% ifelse(is.na(.) == "TRUE","", .)
```

**`r paste(manager_name)`**  
**`r paste(company_name)`**  
`r paste(company_address)`

Dear `r paste(manager_name)`,  

```{r job relative}
job_title <- comp_detail[rownumber,][,"job_title"] %>% unlist() %>% ifelse(is.na(.) == "TRUE","fault title !", .)
job_number <- comp_detail[rownumber,][,"job_number"] %>% unlist() %>% ifelse(is.na(.) == "TRUE","", .)
adv_from <- comp_detail[rownumber,][,"adv_from"] %>% unlist() %>% ifelse(is.na(.) == "TRUE","", .)
post_date <- comp_detail[rownumber,][,"post_date"] %>% pull(.) %>% as.Date(.) %>% format(., "%b %d %Y") %>% ifelse(is.na(.) =="TRUE","", . )
on_logi <- ifelse(is.na(post_date) == T, "on ", "")
```

Re: `r paste(job_title," ",job_number)`  

I am writing to apply for the position of `r paste(job_title)` at `r paste(company_name)`, which was advertised on `r paste(adv_from)` `r paste(on_logi,post_date)`.

```{r what skills I can provide}
skills <- comp_detail[rownumber,][,"what_skills_requred"] %>% unlist()
```

My key assets lie in my `r paste(skills)` skills, which are improved by education, and habit in my free time. More specifically, my strong curiosity encourages me to keep asking questions and solve them via collecting and analysing data.  

```{r reminder}
# Need to add more details here, depends on the requirement of company.
```

I have enclosed my resume to support my application. My professional strengths and accomplishments include:  

```{r}
skill_list <- readxl::read_xlsx(paste0(path,"My Skill list.xlsx"))
skill1 <- skill_list[1,1] # Data analysis & modelling
descrip1 <- skill_list[1,2]
skill2 <- skill_list[2,1] # Problem-Solving
descrip2 <- skill_list[2,2]
skill3 <- skill_list[3,1] # Adaptability
descrip3 <- skill_list[3,2]
skill4 <- skill_list[4,1] # Passion
descrip4 <- skill_list[4,2]
skill5 <- skill_list[5,1] # Communication/Leadership
descrip5 <- skill_list[5,2]
skill6 <- skill_list[6,1] # Attention to detail
descrip6 <- skill_list[6,2]
```

- **`r paste(skill1)`**: `r paste(descrip1)`  
- **`r paste(skill2)`**: `r paste(descrip2)`  
- **`r paste(skill3)`**: `r paste(descrip3)`  
- **`r paste(skill5)`**: `r paste(descrip5)`  
- **`r paste(skill6)`**: `r paste(descrip6)`

```{r skill match}
skill_match <- comp_detail$Skills_match[rownumber]
```

My Skills are perfectly tailored for this position, `r paste(skill_match)`


```{r resarch company}
company_research <- comp_detail$company_research[rownumber]
```

`r paste(company_name)` `r paste(company_research)`  

I would value the opportunity to talk with you more about this position, and how I could use my skills to benefit your organisation.  

Thank you for considering my application. I look forward to hearing from you.  

Yours sincerely,  
  
Wenwei Fei (Tim)
