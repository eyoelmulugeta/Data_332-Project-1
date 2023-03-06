# Data_332-Project-1
# Done By : Eyoel Mulugeta 

## Introduction
This information is a collection of complaints made about businesses, about their consumer financial products and services. The dataset comprises of Consumer Complaints on Financial products and shows how to classify consumer complaints text into these categories: Debt collection, Consumer Loan, Mortgage, Credit card, Credit reporting, Student loan, Bank account or service, Payday loan, Money transfers, Other financial service, Prepaid card.

## Data Dictionary 📖
 1. Complaint ID: Is the identificaion for the people who made comaplints about the business.
 2. Company: The Businesses that faceed complaints. 
 3. Product: classified consumer complaints text into categories.
 4. Issue: The issues the customers faced 
 5. Company response to customer: How the listed companies responded to the customers issues 

### Customer Complaint Data 

# 1. Cleaning data
   
       df= read.csv("Consumer_Complaints.csv")
       saveRDS(df,"Consumer_Complaints.rds")
       df=readRDS("Consumer_Complaints.rds")
  
The downloades files was a CSV file so it needed to be converted into RDS beacuse its a large data file and effiecney is need when condictiong a project with a large data file. 

## Filtering the Data 

      df = df_1 %>%
         select(State, Company, Issue, Company.response.to.consumer, Product) %>%
         drop_na()
         df_2=df_1[1:50000,]

I had to create  a new filtered data farame from the first one. This was done by cleaning up the data and restrict the filter to the columns I intended to use. In order to complete the job more quickly, I also had to filter such that I could only use the top 50,000 rows.

# 2. Setting A sentimental Analysis

          nrc= tidytext::get_sentiments("nrc")
I insatlled and used an NRC sentiment to create the sentiment analysis. 

     df_2= df_1 %>%
          unnest_tokens(word,Company.response.to.consumer) %>%
          anti_join(stop_words)
      df_3 =df_2 %>% 
          inner_join(lexicon) %>% 
           group_by(word) %>% 
           count(sentiment, sort = TRUE) 
I used the Unnest tokens function in order to automatically lower-case the words and remove punctuation from the Company's response to customer column, so it is eaier to comapre and comine with other colmuns. Then create an NRC and bing sentiment lexicon the claculate the sentiment scores. This was done by grouping the words together and do a count of the sentiments. And I filetered all of this into a new data frame. 


<img width="226" alt="Screen Shot 2023-03-05 at 9 55 20 PM" src="https://user-images.githubusercontent.com/112992643/223016941-8f88dd0c-8ec9-483d-b745-16a9ecaa6c98.png">


## Word count by the sentiment using NRC lexicon
   
     lexicon = get_sentiments("nrc")
    df_3 %>%
    group_by(sentiment) %>%
    slice_max(n, n = 10) %>% 
    ungroup() %>%
    mutate(sentiment= reorder(sentiment, n)) %>%
    ggplot(aes(n, sentiment, fill = sentiment)) +
    geom_col(show.legend = FALSE) +
    facet_wrap(~sentiment, scales = "free_y") +
    labs(x = "count",
       y = "sentiment")
![use thi one](https://user-images.githubusercontent.com/112992643/223239769-3d4292fe-d449-4059-84c4-dd24d47e0827.png)

   1. To perform an analysis, the above table needed to be transformed into a chart. 
   2. The NRC lexicon lists associations of words with several emotions and two sentiemnts which are negative and postive. Each lexicon has a list of
      terms          
       and their connections to specific interest groups, including emotions. 
   3. The sentimental analysis comprised of four words and these were grouped into four sentiments. the sentiments were Joy, anticipation positive and   
      negative.
   4. Company's response for cutomers issues had high number of potivive sentiments and antcicipation while the ngative anf joy sentiments were low. The 
      postive sentiments were more than 150,000, ancticpation was more that 120,000, joy and negative were both below 5000. 


## Word Count by sentiment Using the bing lexicon
  
    lexicon = get_sentiments("bing")

    df_3%>%
    ggplot(aes(x=n, y=sentiment)) +
    geom_bar(stat="identity", fill="red")+
    labs(x = "word count", y = "Sentiment")
    geom_text(aes(label=NA), vjust=-0.3, size=3.5)+
    theme_minimal()

![bing plot eed](https://user-images.githubusercontent.com/112992643/223234038-502f2698-37a8-493e-86b8-3a925b349b64.png)

   1. The bing analysis has a more general conclusion than the nrc sentiment 
   2. The Bing Lexicon divides words into positive and negative categories in a binary approach.
   3. It combines all the negative and poisive into one and dispalyed a chart with two bars. 
   4. The postive sentiment which contained the words relief and progress was above 150,000 and the negative which was the untimely was below 5000

# 3.Word Cloud

    df_3 %>%
    inner_join(get_sentiments("bing")) %>%
    count(word, sentiment, sort = TRUE) %>%
    acast(word ~ sentiment, value.var = "n", fill = 0) %>%
    comparison.cloud(colors = c("purple", "blue"),
                   max.words = 100)
                   
![word clloud](https://user-images.githubusercontent.com/112992643/223245855-8040cdcd-28b9-496d-827c-ed510b49f408.png)

  1. The word cloud is group or cluster of text shown in various sizes.
  2. In this word cloud, four emotions with binary sentiments are shown. progress and relief are assigned to the postivie sentiments and untimely is
      associated with the negative sentiment. 
  3. This visualization will allow us to see the most significant positive and negative terms.   
      




















