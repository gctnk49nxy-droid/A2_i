# Assignment Practice 2: Text Data Partitioning: Individual Practice
## Class Information
Name: Dawson T Oliver

Program Name: Assignment_Practice_2_Oliver_Dawson.ipynb

Student Number: 300515143

Class: DTI5125: Data Science Applications

Professor: Dr. Arya Rahgozar

## 1-Requirements
Problem Statement: Given a sample of digital books create partitions of 100 words of the book text, then with those partitions select a random sample of 200 paritions of each book. We need to generalize the program to do this with multiple books and maintain the label as to what book they belong to. 

For this assignment, the purpose is to, given a selection of text from books, chunk the text so 100 words make up a single partition, from within each book randomly select 200 partitions to make up your sample. We need to ensure that each parition can still be traced back to its associated source book. We also want to make sure this program can handle a large number of books. 

## 2-The Way I Solved

The way I solved this problem can be broken down into a series of steps:

1. Access the associated book text. For the purposes of this assignment, we are relying upon the Gutenberg project files here, and I created a function called `retrieve_book` that takes in the name any uses the nltk library to read in the book. The resulting name and book text is stored within a dictionary for processing. Please note that if we want to use other books, that is perfectly accessible, we just need to access the book text and store the name of the book and book text in the associated dictionary. I generalized it for Gutenberg here as this was the dataset repository we are using here. We could read in text files or access other book text other ways through the internet or other libraries.

2. Create the `all_books_df` that will be used to store the samples from all the books we are looking at

3. Using a `for` loop and python function `enumerate` we go through the dictionary containing all the book names and book text. From here, we create the individual partitions of the current book of size `num_words` and take a sample of `num_partitions` of those partitions. We get this resulting dataframe representing a sample of the individual partitions from the function called `create_book_partitions` that takes in the book text along with the number of words that make up a partition and number of parition samples we want to select and returns a dataframe of the sampled partitions of the associated book.

The `create_book_partitions` function does some basic cleaning (removing the title in square parenthesis) using regex patterns, removes punctuation from the text so we can tokenize individual words using the nltk `word_tokenize` function, creates the partitions by grouping `num_words` together, enumerates each of the partitions for tracing purposes, places all partitions into a dataframe, then take a random sample of `num_partitions` to make up the resulting dataframe. We use an `if` statement to ensure there are at least `num_parititons` partitions available in the dataframe or else we take all the partitions available for the book of interest. The resulting dataframe of this function has two columns: `partition_text`: The parititoned text (containing `num_words` number of words), `ind_book_partition_id`: The identifier associated to the partition in the associated book of text.

4. We assign the individual book an alphabetical letter to be the book's identifier, where the mapping is stored in `book_id_mapping`. Then the results are appended to to the resulting `all_books_df`.
   
5. We repeat this process for all books in the dictionary  

## 3-Output
