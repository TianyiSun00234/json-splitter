import os 
import json 
import math

print('Welcome to the JSON Splitter')
print('First, enter the name of the file you want to split')

try: # request file name 
    file_name = input('filename: ') # request input json file 
    f = open(file_name)
    file_size = os.path.getsize(file_name) # get the file size 
    data = json.load(f) 

    if isinstance(data,list): # check whether the file is an array of objects
        data_len = len(data)
        print('Valid JSON file found') 
    else: 
        print("JSON is not an array of objects")
        exit()

except: 
    print('Error loading JSON file ... exiting')
    exit()

# after pathed the three arguments json file hass been loaded into a variable data

# the next step is to split the file 
# split the file based on maximum file size for each chunk
# if the chunck size is smaller than the file, 
# then we will prompt the user and gracefully exit the script.
# get numeric input 
try: 
    mb_per_file = abs(float(input('Enter maximum file size (MB): ')))
except: 
    print('Error entering maximum file size ... exiting')
    exit()
    
# check that file is larger than max size 
if file_size <mb_per_file*1000000:
    print('File smaller than split size, exiting')
    exit()
    
# determine number of filess necessary 
num_files = math.ceil(file_size/(mb_per_file*1000000))
print('mb_per_file', mb_per_file) 
print('file_size', file_size)
print('num_files', num_files)
print('data_len', data_len)
print('File will be split into ', num_files, 'equal parts')
# we have convert the String input to a Float. 
# To finish up, we will calculate, store and print the num of files 
# created based on the maximum file size. 

# the next step is to set up the data structure 
# for holding the split pieces and tthe cutoffs for each piece. 
# use 2d array: 
    # y-axis: # of nested array  
    # x-axis: size of each nested array 
# to find the cutoff points, 
    # lets divide the length of the json array by the # of files. 
# add the length to the end of the array of indices. 

'''
Alternatively, initialize the 
num_files = 
data_len =
''' 
# initialize 2d array
split_data = [[] for i in range(0, num_files)]

# determine the indices of cutoffs in array 
starts = [math.floor (i*data_len/num_files) for i in range(0,num_files)]
starts.append(data_len)

# loop through 2d array 
for i in range(0, num_files): 
    # loop through each range in array 
    for n in range(starts[i], starts[i+1]):
        split_data[i].append(data[i])
        
# create file when section is complete 
    name = os.path.basename(file_name).split('.')[0]+'_'+str(i+1)+'.json'
    print('name', name)
    
    with open(name, 'w+') as outfile: 
        outfile.write(file_name)
        json.dump(split_data[i], outfile)
        print(len(split_data[i]))
        print('--------------------------------------------------------------------')

print('Part',str(i+1),'... completed')
print('Success! Script Completed')
