

In this Git I analyse the San Francisco 2015 criminality dataset with a specific focus on drug related offenses, below this summary is both code and visualisations of the data analysis. The jupyter notebook is included under data_vis.ipynb.


The main findings were:

    - Simple possession of illegal substance is by far the most common drug offense (68.6%), after that possession with intent of sale (26.3%)
    - There is not much of a peak weekday regarding drug offenses registered, though the amount of offenses is generally lower during the weekend. Most likely due to less police presence.
    - The most common illegal narcotic found is methamphetamine, second, third and fourth place go to marijuana, drug paraphernalia (syringes, (crack)pipes, bongs, etc.) and crack/cocaine respectively. Surprisingly, one case of barbiturate sale was reported, an uncommon and frankly outdated drug group.
    - Some shifts in the amount of offenses per drug during the week can be seen, with especially amphetamines being relatively more common in offense reports during the weekend. Surprisingly, cocaine related offenses are least common on saturdays. 

    
    Categories:
    	- Sale (sale or possession with intent of sale
    	- Possession (simple possession for use)
    	- Loitering (loitering/maintaining presence at location known for drug sales)
    	- Intoxication (under influence of drug in public place)
    	- Other (includes transportation of drug and failure to register as an addict or cultivating marijuana)
    

    
What types of drug offenses are most common?
      



![png](/data_vis/output_3_1.png)


    
    Simple possession of illegal substance is by far most common ~68.6%, after that possession with intent of sale (26.3%).
    Intoxication (0.9%), loitering at location of drug sale (1.8%) and transportation/cultivating (2.4%) make up a minor part of the total drug related offenses




    Is there a day of the week where drug-offenses peak?








![png](/data_vis/output_4_2.png)



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


![png](/data_vis/output_7_1.png)




    Are certain drug-types more likely to be involved in arrests during specific days of the week?
    We will focus on the four most common drug types; (crack)cocaine, (meth)amphetamine, marijuana and opiates



    relative occurence of offenses by drug per weekday



![png](/data_vis/output_10_1.png)

