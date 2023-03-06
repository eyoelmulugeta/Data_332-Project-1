# Data_332-Project-1
#Done By : Eyoel Mulugeta 

##Overview
This information is a collection of complaints made about businesses, about their consumer financial products and services. The dataset comprises of Consumer Complaints on Financial products and shows how to classify consumer complaints text into these categories: Debt collection, Consumer Loan, Mortgage, Credit card, Credit reporting, Student loan, Bank account or service, Payday loan, Money transfers, Other financial service, Prepaid card.

###Customer Complaint Data 

#1. Cleaning data
     df= read.csv("Consumer_Complaints.csv")
    saveRDS(df,"Consumer_Complaints.rds")
    df=readRDS("Consumer_Complaints.rds")
  
The downloades files was a CSV file so it needed to be converted into RDS beacuse its a large data file and effiecney is need when condictiong a project with a large data file. 

##Filtering the Data 

      df = df_1 %>%
         select(State, Company, Issue, Company.response.to.consumer, Product) %>%
         drop_na()
         df_2=df_1[1:50000,]

I had to create  a new filtered data farame from the first one. This was done by cleaning up the data and restrict the filter to the columns I intended to use. In order to complete the job more quickly, I also had to filter such that I could only use the top 50,000 rows.

