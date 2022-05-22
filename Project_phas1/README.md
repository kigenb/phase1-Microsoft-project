# MAKING MOVIES AT MICROSOFT

Project overview.

Microsoft have decided to create a new movies studio and they have no idea anything about creating movies.The task is to collect,clean and movie data from different sources such as Box offices,IMDB so that we can provide recomendation and insight to the Head of Microsoft's new movie studio to set up a succesful and profitable movie studio

Data and Exploration.

The data was provided and I choose two data set from the data provided.I sourced data from internet and retrieved the data through web scrapping. The provided data set can be can be located from zippedData folder.

In my research and anlysis I will explore and give answer in the following question:

1.What impact of Directors of movies have impact in the production and the sales of movies

2.What are the most profitable movies and how much shhould invest in movies.

3.What are most succesfull studios in thhe movie industry

4.Which genre is most profitable in the movie industry

Question 1: What impact Directors have on the sale of movies interms of Box Office?

I will select movie_dataframe1 for anlaysis in the above question.I will look at Directors column and Box Office.Using group by I will group Directors column and Box Office In which I will calculate the avarage sales of movies interms of box office by director.Then I will select top 30 Directors in terms of sales.

Find the avarage sales of the movies  by director and select the top 30 Directors
```
selected_movie_data_frame=movie_dataframe1.groupby(['director'],  as_index=False)['box_office'].mean().sort_values(by='box_office', ascending=False)
best_30_director_box_offiice=selected_movie_data_frame.head(30)
best_30_director_box_offiice.head()
```
 Will plot bar graph to visualize avarage sales of movies per Director
 ```
plt.figure(figsize=(14,7))
ax6 = sns.barplot(x=best_30_director_box_offiice['box_office'], y=best_30_director_box_offiice['director'])
plt.xlabel('Revenue interms Box Office', fontsize=14)
plt.ylabel('Director Name', fontsize=14)
plt.title('Average revenue in Box office', fontsize=16);
```

![directors](https://user-images.githubusercontent.com/104420862/169689229-4d9b0f0d-9e45-470d-9734-11568fa9983c.png)

Recomendation: Have analysed the most top 30 director from the industry based on the total sale of the tickets or revenue from box office. From the above analysis I recommend that the Microsoft should hire the best Directors in order for the movies to sale in Box Office which will eventually nets to higher profits.

Question2: What are the most profitable movies and how much should one invest in movies?
To the question above I will select the dataframes that contain ther budget data which is movie_budget.I will calculate the profit and thhe net profit from the data.Then I will look at the correlation between the production budget and the profits of the movies.Finally i will look at the median of the production budget of the movie.
 
 Frst will remove movies that have 0 in the domestic gross and then will calculate the profit and net profit.
 ```
movie_budgett= movie_budgett[movie_budgett['domestic_gross'] !=0]
movie_budgett['profit'] = movie_budgett['worldwide_gross'] - movie_budgett['production_budget']
movie_budgett['net profit margin'] = movie_budgett['profit'] / movie_budgett['production_budget']
```

plot graph of top 30 movies movies agianst their profit


```
plt.figure(figsize=(14,7))
ax6 = sns.barplot(x=profitable_movie['profit'], y=profitable_movie['movie'])
plt.xlabel('Profit', fontsize=14)
plt.ylabel('Movie Name', fontsize=14)
plt.title('Profit Earned in Movies', fontsize=16);
```
![bar chatt for top 30 movies](https://user-images.githubusercontent.com/104420862/169689609-df290ab1-d7b3-4f9d-b286-2a8eb98d8880.png)

Recommendation:From thhe abbove analysis Avatar,Titanic,star wars are the most succesfull movies produced in terms of their net profits.I reccomend that to the MIcrosoft to emulaate the best practices of the best from the above best movies to ensures the succes movies in terms of the net profits

will plott  a scatter plot production budget vs the profits of movies
 ```
 sns.lmplot(x='production_budget', y='profit', data=movie_budgett, height=7, aspect=2)
plt.xlabel('production budget)', fontsize=12)
plt.ticklabel_format(axis='x', style='sci', scilimits=(6,6))
plt.ylabel('Profit earn by movies', fontsize=12)
plt.title('PRODUCTION BUDGET VS PROFIT EARNED BY MOVIES', fontsize=14);
```

![scatter plot for bbudget](https://user-images.githubusercontent.com/104420862/169696179-45c636c1-8580-4a28-9924-fe1f4aafafa5.png)

Recommendation: From the above scatter plot we can see it is positive trend.From analysis we can see that the more money put in movie budget it is likely to generate more profits in movies.I recommend that Microsoft should allocate movies more money in terms of their budget in order to generate more incomes.

Conclussion.We have analysed and thhhen we based my decision of the allocation on my badget based on thhe median so I I recommend that Microsoft should allocate not less than 70 million dollars in a movie.

Question3: Which genres are most productive at the movie indusrty?

I will select movie genre Budget dataframe because it contains the data for analysis.I will calculate profit of each genre ,profit margin and theen the percentage of the profit.
calculate thhe profit of each genre ,profit margin and percentage profit.
```
movie_genre_budget['profit']=movie_genre_budget['worldwide_gross'] - movie_genre_budget['production_budget']
movie_genre_budget['profit_magirn']=movie_genre_budget['profit'] / movie_genre_budget['production_budget']
movie_genre_budget['%_profitt']= movie_genre_budget['profit_magirn'] * 100
movie_genre_budget.sort_values (by='profit',ascending=False)
```
Using group by will calculate the genre profit margin
```
profit_by_movie_genre = profit_by_movie_genre.groupby(['genres'])['profit_magirn'].mean()
profit_by_movie_genre = profit_by_movie_genre.sort_values(ascending=False).head(30)
profit_by_movie_genre.plot.bar(figsize=(30,10))
plt.ylabel('Average Profit ')
plt.title('Average Profit by genre')
```
![profitable genre](https://user-images.githubusercontent.com/104420862/169698321-e615d98e-e9e1-4cab-867d-11794f7288c1.png)

Recomendation: From the above annalysis I recommend to Microsoft shhould allocate budgetts to all genres bbecause they have potential to generate more incomes and profit.The high perfomance genres according to the analysis are Horror,Action,Crime,Thhriller,comedy have succes in terms of their net profits in movie industry

Question4:Which are the most succesfull studios in the movie industry?
In this quesstion I will look at the most succeful studio in thhe world of movie industry. I will analyse the profit and profit p magirns.

 Calculate  profit and net margin of thhe studios
 ```
movie_merge['profit']=movie_merge['worldwide_gross'] - movie_merge['production_budget']
movie_merge['%_profit']=(movie_merge['profit'] / movie_merge['production_budget']) * 100
movie_merge.head()
```

using groupby we caculate the mean of studios
```
profit_by_movie_studio=movie_merge.groupby('studio').mean()
profit_by_movie_studio.head()
```
PLot a graph to show profits of each genre
```
profit_by_movie_studio = profit_by_movie_studio.groupby(['studio'])['profit'].mean()
profit_by_movie_studio = profit_by_movie_studio.sort_values(ascending=False).head(30)
profit_by_movie_studio.plot.bar(figsize=(30,10))
plt.ylabel('Average Profit ')
plt.title('Average Profit by Studio')
```

![top studios interms of profit](https://user-images.githubusercontent.com/104420862/169698422-21c719e8-16e6-44c5-a88f-5b93cc2e299d.png)

Recommendation:That from the data above I recomend is to employ best practices to equivalent to top 10 studios by avarage profit.
Using groupby calculate the net profit mean
```
profit_by_movie_genre1=movie_merge.groupby(['studio'],  as_index=False)['Net profit'].mean().sort_values(by='Net profit', ascending=False)
profit_by_movie_genre1=profit_by_movie_genre1.head(30)
```
plot a graph
```
plt.figure(figsize=(14,7))
ax6 = sns.barplot(x=profit_by_movie_genre1['Net profit'], y=profit_by_movie_genre1['studio'])
plt.xlabel('Net profit', fontsize=14)
plt.ylabel('Studio Name', fontsize=14)
plt.title('Average Net profit by Studio', fontsize=16);
```



![output](https://user-images.githubusercontent.com/104420862/169716877-5ffc5fd7-56f6-486c-97cc-b082cfcbf879.png)


From the above analysis there is difference between the net profit and profit.we could see warner Bross havee hihg much net profits compared to the others which is followed by the UTV nd FD. I recommend that Micrososft should follow the best practises employed by the best movies studios.

