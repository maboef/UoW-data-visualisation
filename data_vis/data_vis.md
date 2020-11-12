```python
import pandas as pd

data_SF = pd.read_csv('sanfrancisco_incidents_summer_2014.csv')
drug_off = data_SF.loc[data_SF['Category'] == 'DRUG/NARCOTIC']

```

In this Git I analyse the San Francisco 2015 criminality dataset with a specific focus on drug related offenses, below this summary is both code and visualisations of the data analysis. 


The main findings were:

    - Simple possession of illegal substance is by far the most common drug offense (68.6%), after that possession with intent of sale (26.3%)
    - There is not much of a peak weekday regarding drug offenses registered, though the amount of offenses is generally lower during the weekend. Most likely due to less police presence.
    - The most common illegal narcotic found is methamphetamine, second, third and fourth place go to marijuana, drug paraphernalia (syringes, (crack)pipes, bongs, etc.) and crack/cocaine respectively. Surprisingly, one case of barbiturate sale was reported, an uncommon and frankly outdated drug group.
    - Some shifts in the amount of offenses per drug during the week can be seen, with especially amphetamines being relatively more common in offense reports during the weekend. Surprisingly, cocaine related offenses are least common on saturdays. 


```python
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline

sales_SF = drug_off.loc[drug_off['Descript'].str.contains("SALE")]
non_sales_SF = drug_off.loc[~drug_off['Descript'].str.contains("SALE")]
poss = non_sales_SF.loc[non_sales_SF['Descript'].str.contains("POSSESSION")]
loit = non_sales_SF.loc[non_sales_SF['Descript'].str.contains("LOITERIN|MAINTAINING")]
infl = non_sales_SF.loc[non_sales_SF['Descript'].str.contains("INFLUENCE")]
other = non_sales_SF.loc[~non_sales_SF['Descript'].str.contains("LOITERING|POSSESSION|MAINTAINING|INFLUENCE")]

p_sales = ((len(sales_SF)/len(drug_off))*100)
p_poss = ((len(poss)/len(drug_off))*100)
p_loit = ((len(loit)/len(drug_off))*100)
p_infl = ((len(infl)/len(drug_off))*100)
p_other = ((len(other)/len(drug_off))*100)

labels = 'Sale', 'Possession', 'Loitering', 'Intoxication', 'Other'
sizes = [p_sales, p_poss,  p_loit, p_infl, p_other]



```


```python
print("\n\nWhat types of drug offenses are most common?\n\n")
print('\033[1m' + "Categories:" + '\033[0m')
print("\t- Sale (sale or possession with intent of sale\n"
     "\t- Possession (simple possession for use)\n"
     "\t- Loitering (loitering/maintaining presence at location known for drug sales)\n"
     "\t- Intoxication (under influence of drug in public place)\n"
     "\t- Other (includes transportation of drug and failure to register as an addict or cultivating marijuana)"
     "\n\n")

pie, ax1 = plt.subplots(figsize=(7,7))
ax1.pie(sizes, labels=labels, autopct='%1.1f%%', textprops={'fontsize': 11}, rotatelabels=True)
ax1.axis('equal')
ax1.set_title("San Francisco 2015: Drug offense types")
plt.show()


print("\nSimple possession of illegal substance is by far most common ~68.6%, after that possession with intent of sale (26.3%).")
print("Intoxication (0.9%), loitering at location of drug sale (1.8%) and transportation/cultivating (2.4%) make up a minor part of the total drug related offenses")
```

    
    
    What types of drug offenses are most common?
    
    
    [1mCategories:[0m
    	- Sale (sale or possession with intent of sale
    	- Possession (simple possession for use)
    	- Loitering (loitering/maintaining presence at location known for drug sales)
    	- Intoxication (under influence of drug in public place)
    	- Other (includes transportation of drug and failure to register as an addict or cultivating marijuana)
    
    



![png](/data_vis/output_3_1.png)


    
    Simple possession of illegal substance is by far most common ~68.6%, after that possession with intent of sale (26.3%).
    Intoxication (0.9%), loitering at location of drug sale (1.8%) and transportation/cultivating (2.4%) make up a minor part of the total drug related offenses



```python
print("Is there a day of the week where drug-offenses peak?")

monday = len(drug_off.loc[drug_off['DayOfWeek'].str.contains("Monday")])
tuesday = len(drug_off.loc[drug_off['DayOfWeek'].str.contains("Tuesday")])
wednesday = len(drug_off.loc[drug_off['DayOfWeek'].str.contains("Wednesday")])
thursday = len(drug_off.loc[drug_off['DayOfWeek'].str.contains("Thursday")])
friday = len(drug_off.loc[drug_off['DayOfWeek'].str.contains("Friday")])
saturday = len(drug_off.loc[drug_off['DayOfWeek'].str.contains("Saturday")])
sunday = len(drug_off.loc[drug_off['DayOfWeek'].str.contains("Sunday")])

days = ['monday', 'tuesday', 'wednesday', 'thursday', 'friday', 'saturday', 'sunday']
off_counts = [monday, tuesday, wednesday, thursday, friday, saturday, sunday]
x_pos=np.arange(len(days))

fig1, ax2 = plt.subplots()

ax2.bar(x_pos, off_counts, align='center')
ax2.set_ylabel('Number of drug-related offenses')
ax2.set_xticklabels([[' '], 'mon', 'tue', 'wed', 'thu', 'fri', 'sat', 'sun'])
ax2.set_title('San Francisco 2015: Drug offenses per weekday')
plt.plot()
```

    Is there a day of the week where drug-offenses peak?





    []




![png](/data_vis/output_4_2.png)



```python
print("What illegal substance is most commonly found?")

print("Categories:\n"
      "- Crack/Cocaine\n"
      "- Opiates\n"
      "- (Meth)amphetamine\n"
      "- Marijuana\n"
      "- Hallucinogens\n"
      "- Paraphernalia\n"
      "- Barbiturates\n"
      "- Unspecified")
```

    What illegal substance is most commonly found?
    Categories:
    - Crack/Cocaine
    - Opiates
    - (Meth)amphetamine
    - Marijuana
    - Hallucinogens
    - Paraphernalia
    - Barbiturates
    - Unspecified



```python
cocaine = drug_off.loc[drug_off['Descript'].str.contains("COCAINE")]
opiates = drug_off.loc[drug_off['Descript'].str.contains("HEROIN|OPIATES|METHADONE|OPIUM")]
amphet = drug_off.loc[drug_off['Descript'].str.contains("AMPHETAMINE")]
marijuana = drug_off.loc[drug_off['Descript'].str.contains("MARIJUANA")]
hallucin = drug_off.loc[drug_off['Descript'].str.contains("HALLUCINOGEN")]
paraphern = drug_off.loc[drug_off['Descript'].str.contains("PARAPHERNALIA")]
barbits = drug_off.loc[drug_off['Descript'].str.contains("BARBITUATES")]
unspec = drug_off.loc[~drug_off['Descript'].str.contains("COCAINE|HEROIN|OPIATES|METHADONE|OPIUM|AMPHETAMINE|MARIJUANA|HALLUCINOGEN|PARAPHERNALIA|BARBITUATES")]
```


```python
substances = ['cocaine', 'opiates', '(meth)amphetamine', 'marijuana', 'hallucinogenics', 'paraphernalia', 'barbiturates', 'unspecified']
off_counts = [len(cocaine), len(amphet), len(marijuana), len(opiates), len(hallucin), len(barbits), len(paraphern), len(unspec)]
x_pos=np.arange(len(substances))

fig2, ax3 = plt.subplots()

ax3.bar(x_pos, off_counts, align='center', width=0.8)
ax3.set_ylabel('Number of offenses')
ax3.set_xlabel('drug involved')
ax3.set_xticklabels([[' '], 'cocaine', '(meth)amph', 'marijuana', 'opiates', 'hallucinogens', 'barbits', 'paraphern', 'unspecified'])

plt.rcParams["figure.figsize"] = (12,6)
ax3.set_title("San Francisco 2015: Contraband found")
plt.plot()
```




    []




![png](/data_vis/output_7_1.png)



```python
print("Are certain drug-types more likely to be involved in arrests during specific days of the week?")
print("We will focus on the four most common drug types; (crack)cocaine, (meth)amphetamine, marijuana and opiates")
```

    Are certain drug-types more likely to be involved in arrests during specific days of the week?
    We will focus on the four most common drug types; (crack)cocaine, (meth)amphetamine, marijuana and opiates



```python
drug_types = [cocaine, opiates, amphet, marijuana]
days = ['monday', 'tuesday', 'wednesday', 'thursday', 'friday', 'saturday', 'sunday']
drugs = ['cocaine', 'opiates', 'amphet', 'marijuana']
drug_dict = {}
c = 0 
for drug in drug_types:
    drug_dict[drugs[c]] = {}
    for day in days:
        count = len(drug.loc[drug['DayOfWeek'].str.contains(day, case=False)])
        drug_dict[drugs[c]][day]=count
    c += 1

drug_df = pd.DataFrame.from_dict(drug_dict)
total = pd.DataFrame(drug_df.sum(axis=1), columns=['total'])
rel_drug = drug_df.div(total['total'], axis=0)
rel_drug = rel_drug.multiply(100)\
```


```python
print("relative occurence of offenses by drug per weekday")
labels = rel_drug.index.values
cocaine_rel = rel_drug['cocaine'].values
opiates_rel = rel_drug['opiates'].values
amphet_rel = rel_drug['amphet'].values
marijuana_rel = rel_drug['marijuana'].values




x1 = np.arange(len(labels))


line1 = plt.plot(x1, cocaine_rel, label='cocaine')
line2 = plt.plot(x1, opiates_rel, label='opiates')
line3 = plt.plot(x1, amphet_rel, label='amphet')
line4 = plt.plot(x1, marijuana_rel, label='marijuana')

plt.xticks(x1, labels)

plt.rcParams["figure.figsize"] = (10,5)
plt.ylabel('relative occurence of offense')
plt.title('Normalized occurence of offense per drug per day')
plt.legend()
plt.show()
```

    relative occurence of offenses by drug per weekday



![png](/data_vis/output_10_1.png)



```python

```
