# Mars Weatherscraping
## Overview
I read HTML code and visited specific websites designed for utilizing web scraping in order to access news and weather data concerning Mars.

## Resources
*Data Source*:

- https://redplanetscience.com
- https://data-class-mars-challenge.s3.amazonaws.com/Mars/index.html

*Software*:
- Splinter
- BeautifulSoup
- Pandas
- Matplotlib
- Jupyter Notebook

## Results
I first used web scraping with Splinter to pull headlines and teasers from articles about Mars.

```text_elems=news_soup.find_all('div', class_='list_text')```

```for title in news_soup.find_all('div', class_='content_title'):```

```for preview in news_soup.find_all('div', class_='article_teaser_body'):```


I then organized the information to be readable in a json file.

```for x in text_elems:
    title = x.find('div', class_='content_title').text
    preview = x.find('div', class_='article_teaser_body').text
    news = {}
    news['title']=title
    news['preview']=preview
    mars_articles.append(news)
```

I then scraped weather data from the Mars Curiosity rover to organize it, analyze it, then export it as a csv file.
```
for rows in mars_data_rows:
    row_data = rows.find_all('td')
    data_list.append(row_data)
```

```
data2 = []
for row in data_list:
    tdlist = []
    for td in row:
        tdlist.append(td.text)
    data2.append(tdlist)
```

```
row_heading = ['id','terrestrial_date', 'sol', 'ls', 'month', 'min_temp', 'pressure']
mars_df = pd.DataFrame(data2, columns=row_heading)
```

I then used what I had scraped to create a Pandas DataFrame:

![marsdataframe](https://github.com/jakatz87/Mars_Weatherscraping/blob/main/Resources/Mars_DataFrame.png)

With the DataFrame, I was able to analyze several data points, such as:
Average Minimum Temperature by Mars Month:

![marsavgtemp](https://github.com/jakatz87/Mars_Weatherscraping/blob/main/Resources/Mars_Avg_Min_Temp.png)

Average Atmospheric Pressure by Mars Month:

![marsavgpress](https://github.com/jakatz87/Mars_Weatherscraping/blob/main/Resources/Mars_Avg_Pressure.png)

I could also use the data to roughly estimate how long one Martian year takes in earth time.  I used:
Solar Longitude:

![marsyearbyls](https://github.com/jakatz87/Mars_Weatherscraping/blob/main/Resources/Mars_Year_by_ls.png)

Daily Minimum Temperatures:

![marsyearbytemp](https://github.com/jakatz87/Mars_Weatherscraping/blob/main/Resources/Mars_Year_by_temp.png)

Both methods show one Martian year is about 23 Earth Months, or between 670 - 690 Earth days.
