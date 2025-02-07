---
layout: page
title: Monthly Reports Application
description: Customizable monthly reports for Main Street Family Medicine, PLLC.
img: assets/img/report.png
redirect:
importance: 1
category: Main Street Family Medicine
related_publications: false
---

In my role at [Main Street Family Medicine](https://www.mainstreetfamilymed.com/), I created an application to genearte monthly reports. I wrote scripts for easily extracting data from our Electronic Medical Record (EMR) and re-running pertinent analyses each month. Using tools such as RStudio and Shiny, I merged these reports into a publishable (yet password-protected) application for internal sharing. The report includes both patient and business data. Work with patient data is helpful to both our nurse practitioner students as they work on their doctorate projects and the rest of our staff as we continually seek to provide relevant and effective care for our patients. The rest of the data provides opportunites to make well-informed business decisions for the future of our clinic.

Watch the demonstration below for a look at how a user can navigate the application and gain insightful data from it. Please note that several reports are concealed from this demonstration for patient and business confidentiality reasons.

When a user navigates to the web application, they are first prompted to enter the password. With the correct password, the app automatically navigates to the second page, titled "PPD Plot." This stands for "Patients per Provider per Day", which has helped us to keep track of how each provider's patient panels have grown so we can know when to on-board new providers and other staff. 

The second report title is hidden. The video shows the title of the third report ("Monthly Revenue Plots"), but the actual plots are not shown. This data has guided us through decisions concerning patient and company relationships, when to pause enrollment, how closed enrollment impacted our company, and when to open enrollment again.

The fourth report details the insurance status of our patients. This led us to begin collecting insurance information from our patients as the report revealed how most patients' status was unknown. As we gather their insurance statuses, we are able to target specific resources for our patients (ex: which hospital systems accept which insurances for which referral specialties, what our cash pay options are for our uninsured patients, etc).

The title of the fifth report is "Patient Demographics and Conditions," but the report itself is not shown for confidentiality reasons. This data has guided us to create free programs and resources designed for the unique needs of our patient population. The final report title is also hidden.

<div class="row justify-content-sm-center">
    <figure>
        <video src="/assets/video/MSFM_Reports_App_No_Audio.mp4" class="img-fluid rounded z-depth-1" width="auto" height="auto" autoplay controls></video>
    </figure>    
</div>

See below for detailed code on the PPD plot.

<div>
    {% highlight r %}
    #PPD plot
    output$PPD_Plot <- renderPlotly({

        #input variables
        thisProvider<-input$Provider
        start_date <- as.Date(input$Dates[1])
        end_date <- as.Date(input$Dates[2])
        hours_worked <- input$HoursWorked
        provider_working <- paste(thisProvider, " Working?", sep="")

        #Make new ds for the selections
        #select whole ds for all days
        if (hours_worked == "All days") {
          PPD_subset <- PPD %>%
            dplyr::filter(Provider == thisProvider,
                          between(Date, start_date, end_date),
                          Count_by_Provider != 0)
        } 
        #select only full days
        else if (hours_worked == "Full days only") {
          PPD_subset <- PPD %>%
            dplyr::filter(Provider == thisProvider,
                          between(Date, start_date, end_date),
                          Count_by_Provider != 0)
          #select only alisha's full days
          if (thisProvider == "Alisha") {
            PPD_subset <- PPD_subset %>%
              dplyr::filter(`Alisha working?` == 1.0)
          } 
          #select only baker's full days
          else if (thisProvider == "Baker") {
            PPD_subset <- PPD_subset %>%
              dplyr::filter(`Baker Working?` == 1.0)
          } 
          #select only lindsey's full days
          else if (thisProvider == "Lindsey") {
            PPD_subset <- PPD_subset %>%
              dplyr::filter(`Lindsey Working?` == 1.0)
          }
          #select only jackie's full days
          else if (thisProvider == "Jackie") {
            PPD_subset <- PPD_subset %>%
              dplyr::filter(`Jackie Working?` == 1.0)
          }
          #select only corrie's full days
          else if (thisProvider == "Corrie") {
            PPD_subset <- PPD_subset %>%
              dplyr::filter(`Corrie Working?` == 1.0)
          }
        }
        #select NON full days
        else if (hours_worked == "Part days only") {
          PPD_subset <- PPD %>%
            dplyr::filter(Provider == thisProvider,
                          between(Date, start_date, end_date),
                          Count_by_Provider != 0)
          #DO NOT select alisha's full days
          if (thisProvider == "Alisha") {
            PPD_subset <- PPD_subset %>%
              dplyr::filter(`Alisha working?` != 1.0)
          } 
          #DO NOT select baker's full days
          else if (thisProvider == "Baker") {
            PPD_subset <- PPD_subset %>%
              dplyr::filter(`Baker Working?` != 1.0)
          } 
          #DO NOT select lindsey's full days
          else if (thisProvider == "Lindsey") {
            PPD_subset <- PPD_subset %>%
              dplyr::filter(`Lindsey Working?` != 1.0)
          }
          #DO NOT select Jackie's full days
          else if (thisProvider == "Jackie") {
            PPD_subset <- PPD_subset %>%
              dplyr::filter(`Jackie Working?` != 1.0)
          }
          #DO NOT select Corrie's full days
          else if (thisProvider == "Corrie") {
            PPD_subset <- PPD_subset %>%
              dplyr::filter(`Corrie Working?` != 1.0)
          }
        }
        

        #make subsets per user input
        if (thisProvider == "Alisha") {
          PPD1 <- PPD_subset %>%
            dplyr::select("Alisha working?", "Date", "Count_by_Provider", "Observation") %>%
            rename(Provider_Working = `Alisha working?`)
        } else if (thisProvider == "Baker") {
          PPD1 <- PPD_subset %>%
            dplyr::select("Baker Working?", "Date", "Count_by_Provider", "Observation") %>%
            rename(Provider_Working = `Baker Working?`)
        } 
        else if (thisProvider == "Lindsey") {
          PPD1 <- PPD_subset %>%
            dplyr::select("Lindsey Working?", "Date", "Count_by_Provider", "Observation") %>%
            rename(Provider_Working = `Lindsey Working?`)
        }
        else if (thisProvider == "Nurse")  {
          PPD1 <- PPD_subset %>%
            dplyr::select("Date", "Count_by_Provider", "Observation") %>%
            mutate(Provider_Working = 1)
        }
        else if (thisProvider == "Jackie")  {
          PPD1 <- PPD_subset %>%
            dplyr::select("Jackie Working?", "Date", "Count_by_Provider", "Observation") %>%
            mutate(Provider_Working = `Jackie Working?`)
        }
        else if (thisProvider == "Corrie")  {
          PPD1 <- PPD_subset %>%
            dplyr::select("Corrie Working?", "Date", "Count_by_Provider", "Observation") %>%
            mutate(Provider_Working = `Corrie Working?`)
        }
        else {
          PPD1 <- PPD_subset %>%
            dplyr::select("Other Provider Here?", "Date", "Count_by_Provider", "Observation") %>%
            rename(Provider_Working = `Other Provider Here?`)
        }
        
        #make another subset for all the providers
        PPD_subset2 = PPD %>%
          filter(Count_by_Provider != 0) %>%
          filter(Provider != "Nurse") %>%
          filter(between(Date, start_date, end_date))
        
        #make tibble for observation and actual date
        Observation_Day_tibble = tibble(
          Observation = seq(1,360,1),
          Day = unique(PPD$Date))
        
        PPD_subset2 = PPD_subset2 %>%
          left_join(Observation_Day_tibble, by = "Observation")
        
        #make the plot
        gg <- ggplot(data = PPD_subset, aes(x=Observation, y=Count_by_Provider)) +
          #PPD_subset2 to include even provider not selected on the side
          geom_point(data = PPD_subset, aes(x=Observation, y=Count_by_Provider, color=Provider, text=paste("Date: ",Date, "<br>","% Day Alisha Worked: ",`Alisha working?`,"<br>","% Day Baker Worked: ",`Baker Working?`, "<br>","% Day Lindsey Worked: ",`Lindsey Working?`, "<br>","% Day Other Worked: ",`Other Provider Here?`, "<br>","% Day Jackie Worked: ",`Jackie Working?`, "<br>","% Day Corrie Worked: ",`Corrie Working?`, sep=""))) +
          #for total provider, do not include nurse visits
          geom_smooth(data = PPD_subset2, aes(x=Observation, y=Total_Provider_Pts), se=FALSE, alpha=0.5,color="aquamarine4")+
          #for selected provider (ifelse depending on if nurse or other provider selected)
          geom_smooth(method="glm", data=PPD1, aes(x=Observation, y=Count_by_Provider), color="black", method.args=list(family="poisson")) + 
          theme_classic()+
          xlab("Date") + 
          ylab("Number of Patients Seen \n(by Selected Provider)") +
          scale_x_continuous(breaks = seq(1,378,21), labels = c("Aug23","Sept23","Oct23","Nov23","Dec23","Jan24","Feb24","March24","April24","May24", "June24", "July24", "Aug24", "Sept24", "Oct24", "Nov24", "Dec24", "Jan25"))+#current max observations = 360 (1/05/25) (need to find how many unique days are in PPD from PPD.Rmd and then update both seq(1,x,21) and labels). Doing it every 21 since 21ish working days a month
          ylim(0,17) + 
          theme(
            axis.title.x = element_blank()
          )
        
          ggplotly(gg) %>%
            layout(title = list(text = paste0('<br>',
              paste("PPD for ", thisProvider, " between ", as.character(start_date), " & ", as.character(end_date), sep=""),
              '<br>',
              '<sup>',
              '(black line = avg PPD for provider selected; green = total number patients seen per day)', 
              '<br>',
              '<sup>'))
     })


    {% endhighlight %}
</div>

NOTE: Thank you to [Canva](https://www.canva.com/) for the stock report image used for this project.


