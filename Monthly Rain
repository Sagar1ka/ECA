# https://www.ecad.eu/dailydata/index.php

import os
import matplotlib.pyplot as plt

input_dir = r"C:\data\ECA\ECA_blended_custom"
output_dir = input_dir + "\\" + "out"

for input_file in os.listdir(input_dir):
    if "RR" not in input_file: continue
    print ("--------------------------")
    print (input_file)

    InputTextfile = open(input_dir + "\\" + input_file,"r")

    rain_dict = {}
    for line in InputTextfile:
        if len(line.split(",")) < 4: continue
        if "RR" in line: continue  
        #if "0528" in line:
        #    print (line[:-1])
        station, date , rain, quality = line[:-1].split(",")
        if int(quality) != 0: continue
        rain_dict[date] = float(rain)

    #--------------------------------    
    #2. Print statistics for each station
    print (len(rain_dict), "days")
    print (int(len(rain_dict)/365), "years")
    print (sum(rain_dict.values()),"mm of rain")
    print ("Average rain per year", sum(rain_dict.values())/ len(rain_dict) * 365 / 10) 
    
    #--------------------------------
    #3. Print Top 10 Rainy Days + Write to Textfile
    OutTextfile = open(output_dir + "\\" + input_file.replace(".txt","_out.txt"),"w")
    print (sorted(rain_dict, key=rain_dict.get, reverse=True)[:5])
    for date in sorted(rain_dict, key=rain_dict.get, reverse=True)[:10]:
        print (date, rain_dict[date]/10)
        OutTextfile.write(str(date) +","+ str(rain_dict[date]/10)+ "\n")
    
    #--------------------------------
    #4. Plot monthly rain
    montly_rain_list = []
    years = range (1901, 2024)
    month = 4
    for year in years:      
        rain = 0
        for day in range (1,32):
            date = str(year) + str(month).zfill(2) + str(day).zfill(2)
            if date in rain_dict:
                rain = rain + rain_dict[date]
        montly_rain_list.append(rain)
    #print (montly_rain_list)
    
    fig, ax = plt.subplots()
    ax.bar(years, (montly_rain_list)) #sorted
    plt.show()
   
    InputTextfile.close()
    OutTextfile.close()
