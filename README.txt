I spent today working on my portfolio project for the Python 3 Data Visualization Skill Path. I found data on renewable energy source generation and usage from 1965-2021, sorted by country and region.

I condensed the data down to 6 continents and total world generation of renewable energy sources including solar, wind, hydro, and geo/bio/other by TWh. 

The questions I wanted to answer with this project included:

From 1965 to 2021, what continent has generated the most solar energy by TWh?
From 1965 to 2021, what continent has generated the most wind energy by TWh?
From 1965 to 2021, what continent has generated the most hydro energy by TWh?
From 1965 to 2021, what continent has generated the most bio/geo/other energy by TWh?

From 1965-2000, what type of renewable energy source was generated the most?
From 2000-2021, what type of renewable energy source was generated the most?

What renewable energy source has Africa produced the most of since 1965?
What renewable energy source has Asia produced the most of since 1965?
What renewable energy source has Australia produced the most of since 1965?
What renewable energy source has Europe produced the most of since 1965?
What renewable energy source has North America produced the most of since 1965?
What renewable energy source has South/Central America produced the most of since 1965?

I made this whole project in JupyterLab with matplotlib and Seaborn visualization tools. 
I began with importing the required modules (Pyplot, Pandas, and Seaborn). Then I imported the data using Pandas.

{
# Data Source - https://www.kaggle.com/datasets/belayethossainds/renewable-energy-world-wide-19652022?resource=download

energy = pd.read_csv('modern-renewable-energy-consumption.csv')
# NaN replaced with float for cleaner visuals
energy2 = pd.read_csv('modern-renewable-energy-consumption - nanless.csv')
# Total data for pie charts
energy3 = pd.read_csv('modern-renewable-energy-consumption - totals.csv')

energy.head(10)
energy2.head(10)
energy3.head(10)

sns.pairplot(data=energy2, hue="Entity")
plt.savefig('Potential Correlations Pairplot.png')
plt.show()
}

I then made a subplot of 4 Seaborn lineplots displaying growth of energy source generation,
from 1965-2000, sorted by continent

{
# 1965-2000 Renewable Energy Generation 

sns.set_style("whitegrid")
x = plt.figure(figsize=(13,11), facecolor='white')
x.suptitle('Renewable Energy Generation TWh by Country (1965-2000)', fontsize=20)
x.supxlabel('Year')

# Solar

plt.subplot(2,2,1)
ax = sns.lineplot(data=energy2, x='Year', y='Solar Generation - TWh', estimator='mean', hue='Entity')
leg = plt.legend(loc=[0.01,0.585], frameon=True)
plt.xlabel('')
ax.set_xlim((1965, 2000))
ax.set_xticks([1965, 1970, 1975, 1980, 1985, 1990, 1995, 2000])

# Wind

plt.subplot(2,2,2)
ax = sns.lineplot(data=energy2, x='Year', y='Wind Generation - TWh', hue='Entity', estimator='mean', legend=False)
plt.xlabel('')
ax.set_xlim((1965, 2000))
ax.set_xticks([1965, 1970, 1975, 1980, 1985, 1990, 1995, 2000])

# Hydro

plt.subplot(2,2,3)
ax = sns.lineplot(data=energy2, x='Year', y='Hydro Generation - TWh', hue='Entity', estimator='mean', legend=False)
plt.xlabel('')
ax.set_xlim((1965, 2000))
ax.set_xticks([1965, 1970, 1975, 1980, 1985, 1990, 1995, 2000])

# Other

plt.subplot(2,2,4)
ax = sns.lineplot(data=energy2, x='Year', y='Geo Biomass Other - TWh', hue='Entity', estimator='mean', legend=False)
plt.xlabel('')
ax.set_xlim((1965, 2000))
ax.set_xticks([1965, 1970, 1975, 1980, 1985, 1990, 1995, 2000])

plt.savefig('Lineplot 1965-2000.png')
plt.show()
}

I then made another subplot of 4 Seaborn lineplots displaying growth of energy source generation,
from 2000-2020, sorted by continent

{
# 2000-2020 Renewable Energy Generation 

sns.set_style("whitegrid")
x = plt.figure(figsize=(13,11), facecolor='white')
x.suptitle('Renewable Energy Generation TWh by Country (2000-2020)', fontsize=20)
x.supxlabel('Year')

# Solar

plt.subplot(2,2,1)
ax = sns.lineplot(data=energy2, x='Year', y='Solar Generation - TWh', estimator='mean', hue='Entity')
leg = plt.legend(loc=[0.01,0.585], frameon=True)
plt.xlabel('')
ax.set_xlim((2000, 2020))
ax.set_xticks([2000, 2002, 2004, 2006, 2008, 2010, 2012, 2014, 2016, 2018, 2020])

# Wind

plt.subplot(2,2,2)
ax = sns.lineplot(data=energy2, x='Year', y='Wind Generation - TWh', hue='Entity', estimator='mean', legend=False)
plt.xlabel('')
ax.set_xlim((2000, 2020))
ax.set_xticks([2000, 2002, 2004, 2006, 2008, 2010, 2012, 2014, 2016, 2018, 2020])

# Hydro

plt.subplot(2,2,3)
ax = sns.lineplot(data=energy2, x='Year', y='Hydro Generation - TWh', hue='Entity', estimator='mean', legend=False)
plt.xlabel('')
ax.set_xlim((2000, 2020))
ax.set_xticks([2000, 2002, 2004, 2006, 2008, 2010, 2012, 2014, 2016, 2018, 2020])

# Other

plt.subplot(2,2,4)
ax = sns.lineplot(data=energy2, x='Year', y='Geo Biomass Other - TWh', hue='Entity', estimator='mean', legend=False)
plt.xlabel('')
ax.set_xlim((2000, 2020))
ax.set_xticks([2000, 2002, 2004, 2006, 2008, 2010, 2012, 2014, 2016, 2018, 2020])

plt.savefig('Lineplot 2000-2020.png')
plt.show()
}

I then made a subplot of 4 pie charts that show the total generated TWh from 1965-2021 of each energy source, sorted by country

{
# 1965-2021 Total Renewable Energy Generation 

sns.set_style("whitegrid")
x = plt.figure(figsize=(13,11), facecolor='white')
plt.suptitle('Total Resource Generation TWh by Country (1965-2021)', fontsize=20)

# Solar

plt.subplot(2,2,1)
ax = plt.pie(x=energy3['Solar Generation - TWh'], labels=energy3['Entity'], shadow=True)
plt.xlabel('')
plt.title('Solar Total TWh')

# Wind

plt.subplot(2,2,2)
ax = plt.pie(x=energy3['Wind Generation - TWh'], labels=energy3['Entity'], shadow=True)
plt.xlabel('')
plt.title('Wind Total TWh')

# Hydro

plt.subplot(2,2,3)
ax = plt.pie(x=energy3['Hydro Generation - TWh'], labels=energy3['Entity'], shadow=True)
plt.xlabel('')
plt.title('Hydro Total TWh')

# Other

plt.subplot(2,2,4)
ax = plt.pie(x=energy3['Geo Biomass Other - TWh'], labels=energy3['Entity'], shadow=True)
plt.xlabel('')
plt.title('Geo/Biomass/Other Total TWh')

plt.savefig('Pie_Charts 1965-2021.png')
plt.show()
}

Back to the questions...

From 1965 to 2021, what continent has generated the most solar energy by TWh?
Answer: Asia
From 1965 to 2021, what continent has generated the most wind energy by TWh?
Answer: Europe
From 1965 to 2021, what continent has generated the most hydro energy by TWh?
Answer: Asia
From 1965 to 2021, what continent has generated the most bio/geo/other energy by TWh?
Answer: North America

From 1965-2000, what type of renewable energy source was generated the most?
Answer: Hydro
From 2000-2021, what type of renewable energy source was generated the most?
Answer: Hydro still, but wind and solar have higher growth rates

What renewable energy source has Africa produced the most of since 1965?
Answer: Hydro
What renewable energy source has Asia produced the most of since 1965?
Answer: Solar
What renewable energy source has Australia produced the most of since 1965?
Answer: Solar
What renewable energy source has Europe produced the most of since 1965?
Answer: Wind
What renewable energy source has North America produced the most of since 1965?
Answer: Hydro
What renewable energy source has South/Central America produced the most of since 1965?
Answer: Hydro


Conclusions:

From 1965-2000, the main sources of renewable energy were hydro and beo/bio/other. Hydro power has been used worldwide since the 1880s, and still is the most largely used source of renewable energy. 

By 2000, large countries began producing solar and wind energy, displayed by an immense growth rate, beginning in approximately 2008-2010. 

Wind power is projected to have the largest growth rate of any renewable energy source, due to its versatile platform. Hydro energy has a stagnant growth rate, possibly because cheaper, more versatile sources are available. 

I was surpised by how little wind and solar power has been produced since 2000. I expected the combination of the two to surpass total hydro power. However, the combination of solar, wind, and geo/bio/other doesn't even add up to half of the total energy produced by hydro. 

The data was only a range from 1965-2021. It is 2023, so growth rates might have changed slightly since this data was gathered. There is plenty more data on renewable energy sources, and how they have impacted global energy production. Areas for further exploration include energy consumption and total energy share. I can also compare by country instead of continent in order to visualize the difference in renewable energy production by first-world and third-world countries. 

That's all folks!

- Rhett