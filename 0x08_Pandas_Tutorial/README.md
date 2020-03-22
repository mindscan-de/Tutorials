# Pandas Tutorial / Pandas Cookbook

Since there are a lot of pandas resources online, I won't try to write a better or more complete one. I simply want to collect some of the code snippets
which I found useful and where I had to do at least some minor research on how to achive a certain functionality - which I don't want to repeat.

## Load json-lines (.jsonl) data files

JSON lines (.jsonl) is a format, which contains a complete json string in each line. This allows you to read and process data as a stream instead as one single document. 
The json documents also get larger when the datasets grow in size.

~~~
# where to get the data
fullFilename = os.path.join(dataset_directory, 'methodDataset.jsonl')

# each line contains one json document
df = pd.read_json(fullFilename, lines=True)
~~~



## Useful Resources

	* https://pandas.pydata.org/docs/pandas.pdf