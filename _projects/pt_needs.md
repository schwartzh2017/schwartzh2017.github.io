---
layout: page
title: Patient Needs Survey Analysis
description: Analyzing results from patient needs survey.
img: /assets/img/needs.jpg
redirect:
importance: 2
category: New Heights Clinic
related_publications: false
---

To better assist New Heights Clinic patients, we asked patients to fill out a survey informing us of their needs. After collecting basic demographic information, we gathered a holistic look at patients and asked about a variety of topics, from healthcare needs to food insecurity to transportation capabilities. I used the results, along with knowledge of the clinic functions, to determine the next best steps for our team as we aim to improve understanding of and care for our patients.

Check out the project results [here.](/assets/html/Patient_Needs_2024.html)

See below for example code on how I imputed missing data and predicted federal poverty level.

<div>
    {% highlight r %}

        # More Cleaning
        ## Impute where NA > 20%
        ### Employment Status

        #select necessary columns
        ds_emp = ds %>% dplyr::select(gender, head_household, marital_status, have_ins, employment_status)
        ds_emp2 = ds %>% dplyr::select(employment_status)

        #first understand the missing data
        aggr(ds_emp2, col=c('navyblue','red'), numbers=TRUE, sortVars=TRUE, labels=names(data), cex.axis=.7, gap=3, ylab=c("Histogram of missing data","Pattern")) #80% of data is complete, 95% is what we need to not impute

        #combine with imputed pov ds to give a better estimate for imputation
        ds_emp_final=bind_cols(imp_ds_pov,ds_emp)

        #impute with pmm method in mice to impute since both mo_income and household_size are normally distributed
        ds_emp_final_imp <- mice(ds_emp_final,m=5,maxit=50,method = "pmm",seed=500)
        ds_emp_final_imp = complete(ds_emp_final_imp,1)

        
        ##################
        ##################

        # More Cleaning
        ## Find Fed Pov Level

        #read in and clean up poverty data. 
        pov = read_csv("/Users/Haleigh/Documents/NH/Reports/Demo/Fed_Pov_2024.csv") #downloaded from https://aspe.hhs.gov/topics/poverty-economic-mobility/poverty-guidelines (click on "A Chart with percentages (e.g., 125 percent) of the guidelines (PDF"))

        pov = pov %>%
        mutate(across(ends_with("%"), ~ str_remove_all(.x, "[$,]") %>% as.numeric())) %>%
        rename(household_size = `Household/\nFamily Size`)

        ###################

        # Function to predict poverty level

        predict_poverty_level <- function(household_size, mo_income, pov) {
        # If household size is NA, return NA
        if (is.na(household_size) | is.na(mo_income)) {
            return(NA)
        }
        
        # Get the relevant thresholds for the household size
        thresholds <- pov[pov$household_size == household_size, ]
        
        if (mo_income <= thresholds$`25%`) {
            return("25%")
        } else if (mo_income <= thresholds$`50%`) {
            return("50%")
        } else if (mo_income <= thresholds$`75%`) {
            return("75%")
        } else if (mo_income <= thresholds$`100%`) {
            return("100%")
        } else if (mo_income <= thresholds$`125%`) {
            return("125%")
        } else if (mo_income <= thresholds$`130%`) {
            return("130%")
        } else if (mo_income <= thresholds$`133%`) {
            return("133%")
        } else if (mo_income <= thresholds$`135%`) {
            return("135%")
        } else if (mo_income <= thresholds$`138%`) {
            return("138%")
        } else if (mo_income <= thresholds$`150%`) {
            return("150%")
        } else if (mo_income <= thresholds$`175%`) {
            return("175%")
        } else if (mo_income <= thresholds$`180%`) {
            return("180%")
        } else if (mo_income <= thresholds$`185%`) {
            return("185%")
        } else if (mo_income <= thresholds$`200%`) {
            return("200%")
        } else if (mo_income <= thresholds$`225%`) {
            return("225%")
        } else if (mo_income <= thresholds$`250%`) {
            return("250%")
        } else if (mo_income <= thresholds$`275%`) {
            return("275%")
        } else if (mo_income <= thresholds$`300%`) {
            return("300%")
        } else if (mo_income <= thresholds$`325%`) {
            return("325%")
        } else if (mo_income <= thresholds$`350%`) {
            return("350%")
        } else if (mo_income <= thresholds$`375%`) {
            return("375%")
        } else if (mo_income <= thresholds$`400%`) {
            return("400%")
        } else if (mo_income <= thresholds$`500%`) {
            return("500%")
        } else if (mo_income <= thresholds$`600%`) {
            return("600%")
        } else if (mo_income <= thresholds$`700%`) {
            return("700%")
        } else if (mo_income <= thresholds$`800%`) {
            return("800%")
        } else if (mo_income <= thresholds$`1000%`) {
            return("1000%")
        } else {
            return(">1000%")
        }
        }

        ##################

        #predict
        ds_pov_pred = ds_pov %>%
        rowwise() %>%
        mutate(poverty_level = predict_poverty_level(household_size, mo_income, pov))

        #convert to numeric for easier graphing
        ds_pov_pred = ds_pov_pred %>%
        mutate(poverty_level = as.numeric(str_remove_all(poverty_level, "%")))

        #add on MoE
        ds_pov_pred=ds_pov_pred %>%
        mutate(moe_low = poverty_level-(poverty_level*0.05),
                moe_high = poverty_level+(poverty_level*0.05))

    {% endhighlight %}
</div>

NOTE: Thank you to [iStock by Getty Images](https://www.istockphoto.com/) for the stock image used for this project.