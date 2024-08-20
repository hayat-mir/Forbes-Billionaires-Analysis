1  . Which sector has the most number of billionaires?
source = df['Source'].value_counts().head(10)
plt.figure(figsize=(15,9))
sns.barplot(x=source.index, y=source.values, alpha=0.8)
plt.title('Number of billionaires - sector wise', fontsize=18)
plt.ylabel('Number of billionaires', fontsize=12)
plt.xlabel('Sector', fontsize=12)
plt.show()
executed in 218ms, finished 14:43:43 2024-03-21

2  Does a college degree required to become a billionaire?
df['Education'] = df['Education'].fillna('empty')
master = 0
bachelor = 0
phd = 0
drop_out = 0
others = 0
unknown = 0
for i in df['Education']:
  if 'Ph.D' in i or 'Doctorate' in i:
    phd += 1
  elif 'Master' in i or 'MBA' in i:
    master += 1
  elif 'Bachelor' in i:
    bachelor += 1
  elif 'Drop Out' in i:
    drop_out += 1
  elif i == 'empty':
    unknown += 1
  else:
    others += 1
​
bachelor_percent = bachelor/(bachelor+master+phd+drop_out+others)*100
master_percent = master/(bachelor+master+phd+drop_out+others)*100
phd_percent = phd/(bachelor+master+phd+drop_out+others)*100
dropout_percent = drop_out/(bachelor+master+phd+drop_out+others)*100
others_percent = others/(bachelor+master+phd+drop_out+others)*100
​
print(f'Around {round(bachelor_percent)}% of the billionaires have only done bachelors degree')
print(f'Around {round(master_percent)}% of the billionaires have done masters degree')
print(f'Around {round(phd_percent)}% of the billionaires have done PHD degree')
print(f'Around {round(dropout_percent)}% of the billionaires have dropped out of the college')
executed in 20ms, finished 14:43:43 2024-03-21
Around 48% of the billionaires have only done bachelors degree
Around 32% of the billionaires have done masters degree
Around 6% of the billionaires have done PHD degree
Around 6% of the billionaires have dropped out of the college
labels = ['Bachelors', 'Masters', 'PHD', 'Dropout', 'Others']
sizes = [bachelor_percent, master_percent, phd_percent, dropout_percent, others_percent]
plt.figure(figsize=(13,8))
plt.pie(sizes, labels=labels,autopct='%1.1f%%',startangle=140)
plt.title('Billionaires with college degrees', fontsize=14)
plt.show()
executed in 113ms, finished 14:43:43 2024-03-21

3  Where to study to become a billionaire?
final_bachelor = {}
final_master = {}
for i in df['Education']:
  j = i.split(';')
  if len(j) == 1 and 'Bachelor' in j[0]:
    new = j[0].split(',')
    if new[-1] in final_bachelor:
      final_bachelor[new[-1]] += 1
    else:
      final_bachelor[new[-1]] = 1
  elif len(j) == 2 and 'Master' in j[0]:
    new = j[0].split(',')
    if new[-1] in final_master:
      final_master[new[-1]] += 1
    else:
      final_master[new[-1]] = 1
  elif len(j) == 2 and 'Master' in j[1]:
    new = j[1].split(',')
    if new[-1] in final_master:
      final_master[new[-1]] += 1
    else:
      final_master[new[-1]] = 1
​
sort_bachelor = dict(sorted(final_bachelor.items(),key=lambda x:x[1],reverse = True)[:10])
sort_master = dict(sorted(final_master.items(),key=lambda x:x[1],reverse = True)[:10])
print('No. of billionaires who have done Bachelors at:', sort_bachelor)
print('No. of billionaires who have done Masters at:', sort_master)
executed in 16ms, finished 14:43:43 2024-03-21
No. of billionaires who have done Bachelors at: {' Stanford University': 12, ' Harvard University': 10, ' University of Southern California': 8, ' The Wharton School': 7, ' Bombay University': 7, ' University of Washington': 5, ' Yale University': 5, ' Delhi University': 5, ' Cornell University': 5, ' University of Pennsylvania': 4}
No. of billionaires who have done Masters at: {' Harvard University': 21, ' Harvard Business School': 19, ' Stanford University': 12, ' Columbia Business School': 10, ' Stanford Graduate School of Business': 9, ' Massachusetts Institute of Technology': 7, ' The Wharton School': 6, ' Leonard N. Stern School of Business': 6, ' Columbia University': 5, ' Samuel Curtis Johnson Graduate School of Management': 3}
plt.figure(figsize=(13,7))
plt.bar(*zip(*sort_bachelor.items()))
plt.title('Number of Billionaires who have done Bachelors', fontsize=18)
plt.ylabel('Number of billionaires', fontsize=12)
plt.xlabel('University name', fontsize=12)
plt.xticks(rotation=90)
plt.show()
executed in 198ms, finished 14:43:44 2024-03-21

plt.figure(figsize=(13,7))
plt.bar(*zip(*sort_master.items()))
plt.title('Number of Billionaires who have done Masters', fontsize=18)
plt.ylabel('Number of billionaires', fontsize=12)
plt.xlabel('University name', fontsize=12)
plt.xticks(rotation=90)
plt.show()
executed in 178ms, finished 14:43:44 2024-03-21

4  Number of Billionaries - Age wise:
age = {'n0s':0, '10s':0, '20s':0, '30s':0, '40s':0, '50s':0, '60s':0, '70s':0, '80s':0, '90s':0, 'above':0}
for i in df['Age']:
  age[str(i)[0] + '0s'] += 1
​
for k,v in age.items():
  if k == 'n0s' or k == 'above':
    pass
  else:
    print(f'Number of billionaires who are in their {k}:',v)
executed in 17ms, finished 14:43:44 2024-03-21
Number of billionaires who are in their 10s: 0
Number of billionaires who are in their 20s: 0
Number of billionaires who are in their 30s: 20
Number of billionaires who are in their 40s: 71
Number of billionaires who are in their 50s: 196
Number of billionaires who are in their 60s: 291
Number of billionaires who are in their 70s: 250
Number of billionaires who are in their 80s: 135
Number of billionaires who are in their 90s: 32
age1 = age.copy() 
if 'n0s' in age1:
    del age1['n0s']
if 'above' in age1:
    del age1['above']
​
plt.figure(figsize=(11,7))
plt.bar(*zip(*age1.items()))
plt.title('Billionaires with their age', fontsize=18)
plt.ylabel('Number of billionaires', fontsize=12)
plt.xlabel('Age', fontsize=12)
plt.show()
executed in 131ms, finished 14:43:44 2024-03-21

5  Number of Self made billionaries:
print("Number of billionaires who are self made: ",df['Self_made'].sum())
print("Number of billionaires who are not self made: ",len(df['Self_made']) - df['Self_made'].sum())
executed in 15ms, finished 14:43:44 2024-03-21
Number of billionaires who are self made:  708
Number of billionaires who are not self made:  287
plt.figure(figsize=(8, 5))
sns.barplot(x=['Self-Made', 'Non self-made'], y=[df['Self_made'].sum(), len(df) - df['Self_made'].sum()], alpha=0.8)
plt.title('Self-made vs Non self-made billionaires', fontsize=18)
plt.ylabel('Number of billionaires', fontsize=12)
plt.show()
executed in 97ms, finished 14:43:44 2024-03-21

6  Where do younger billionaires live?
df1 = df[df['Age'] <= 35]
young = df1['Country'].value_counts().head(10)
​
plt.figure(figsize=(15, 9))
sns.barplot(x=young.index, y=young.values, alpha=0.8)
plt.title('Young Billionaires (aged below 35) live in', fontsize=18)
plt.ylabel('Number of billionaires', fontsize=12)
plt.xlabel('Country', fontsize=12)
plt.show()
executed in 130ms, finished 14:43:44 2024-03-21

7  Number of billionaires in each relationship category
status = df['Status'].value_counts()
plt.figure(figsize=(15,9))
sns.barplot(x=status.index, y=status.values, alpha=0.8)
plt.title('Number of billionaires in each relationship category', fontsize=18)
plt.ylabel('Number of billionaires', fontsize=12)
plt.xlabel('Relationship status', fontsize=12)
plt.show()
executed in 164ms, finished 14:43:44 2024-03-21

8  How many billions are contributed by the billionaires to the country?
contributed = df.groupby('Country')['NetWorth'].sum().sort_values(ascending=False).head(10)
plt.figure(figsize=(15,9))
sns.barplot(x=contributed.index, y=contributed.values, alpha=0.8)
plt.title('NetWorth of billionaires - country wise', fontsize=18)
plt.ylabel('Billions', fontsize=12)
plt.xlabel('Country', fontsize=12)
plt.show()
executed in 165ms, finished 14:43:45 2024-03-21

9  Which city contains more billionaires?
city = df['Residence'].value_counts().head(10)
plt.figure(figsize=(13,7))
sns.barplot(x=city.index, y=city.values, alpha=0.8)
plt.title('Number of billionaires - city wise', fontsize=18)
plt.ylabel('Number of Billionaires', fontsize=12)
plt.xlabel('City', fontsize=12)
plt.xticks(rotation=90)
plt.show()
executed in 232ms, finished 14:43:45 2024-03-21

10  How many billionaire families are there?
family = 0
for i in df['Name']:
  j = i.split()
  if j[-1] == 'family':
    family += 1
print('Number of billionaire families: ', family)
executed in 15ms, finished 14:43:45 2024-03-21
Number of billionaire families:  85
​
