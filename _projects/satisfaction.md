---
layout: page
title: Patient Satisfaction Survey Analysis
description: Analyzing results from patient satisfaction surveys across time.
img: /assets/img/survey.jpg
redirect:
importance: 3
category: New Heights Clinic
related_publications: false
---

Every 6 months, NHC is required to complete a patient satisfaction survey. Surveys ask 14 questions which all range from 1 (worst) to 4 (best). There is a section to leave additional comments. I analyzed results from both the most recent data and data aggregated since we began collecting the surveys in 2017. I used the results, along with knowledge of the clinic functions, to determine the next best steps for our team as we aim to improve care for our patients. For a summary of the most relevant findings, check out the results [here.](/assets/html/NHC_pt_satis_survey_alltime.html)

See below for some basic statistic methods I used to detemine significance of question responses across time.

<div>
    {% highlight r %} 
        #t test for graph #2
        ttest_alltime = ds %>%
        filter(year != "12/2024") %>%
        dplyr::select(Response, Question_no) %>%
        mutate(group = "alltime")

        ttest_current =ds %>%
        filter(year == "12/2024") %>%
        dplyr::select(Response, Question_no) %>%
        mutate(group = "current")

        ttest_combo=bind_rows(ttest_alltime,ttest_current)

        mod_mean=aov(Response ~ group*Question_no, data=ttest_combo) 
        tukey_mod_mean = TukeyHSD(mod_mean, conf.level=0.95)
        tukey_mod_mean

        tukey_results_mean <- as.data.frame(tukey_mod_mean$`group:Question_no`)
        tukey_results_mean %>%
        filter(`p adj` <= 0.05) #diff between the same Q across years is not sig


        ##################
        ##################
        

        # Are the responses different from each question across years?

        #plot
        ds %>%
        ggplot()+
        geom_boxplot(aes(x=Question_no,y=Response))+
        theme_classic() 


        #tukey test 
        mod=aov(Response~year*Question_no,data=ds)
        tukey_mod = TukeyHSD(mod,conf.level = 0.95)
        tukey_mod


        #compare across years
        tukey_results <- as.data.frame(tukey_mod$`year:Question_no`)
        tukey_results %>%
        filter(`p adj` < 0.3) #none are significant, closest to sig was 0.25 and it wasn't even between the same Q


        #compare just question_no
        tukey_results2 = as.data.frame(tukey_mod$Question_no)
        tukey_results2 %>%
        filter(`p adj` < 0.05) #question 3 and 4 are significantly lower than the majority of the others. Q2 is sig diff from only two other questions
    
    {% endhighlight %}
</div>

NOTE: Thank you to [iStock by Getty Images](https://www.istockphoto.com/) for the stock survey image used for this project.