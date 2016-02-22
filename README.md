# Exploring Entity Resolution with Dedupe in Python

This walk-through uses [Jupyter Notebook](http://jupyter.readthedocs.org/en/latest/install.html) and [Pandas](https://readthedocs.org/projects/pandas/) (and of course, [Dedupe](https://dedupe.readthedocs.org/en/latest/)) to explore some initial approaches to deduplication and entity resolution with the Python library Dedupe.

Please make sure you have Jupyter and Pandas installed before we move on.

```bash
pip install jupyter
pip install pandas
```


## Dedupe Examples

These are example scripts for [dedupe](https://github.com/datamade/dedupe), a library that uses machine learning to perform de-duplication and entity resolution quickly on structured data.

To get these examples:
```bash
git clone https://github.com/DistrictDataLabs/dedupe-examples.git
cd dedupe-examples
```

Now we'll launch Jupyter and open up the file called "DDRL_EntResLab.ipynb":
```bash
jupyter notebook
```


### [CSV example](http://datamade.github.com/dedupe-examples/docs/csv_example.html) - early childhood locations

## Testing out `dedupe`

Let's experiment with using the `dedupe` library to try cleaning up our file.    

To get `dedupe` running, we'll need to install [Unidecode](https://pypi.python.org/pypi/Unidecode), [Future](https://pypi.python.org/pypi/future), and [Dedupe](https://dedupe.readthedocs.org/en/latest/).

In your terminal:
```bash
pip install unidecode
pip install future
pip install dedupe
```    


Then we'll run the csv_example.py file to see what dedupe can do:

```bash
python csv_example.py
```

You can see that `dedupe` is a command line application that will prompt the user to engage in active learning by showing pairs of entities and asking if they are the same or different.

    Do these records refer to the same thing?
    (y)es / (n)o / (u)nsure / (f)inished

Let's start training!
Use 'y', 'n' and 'u' keys to flag duplicates for active learning.    

When you are finished, enter 'f' to quit.    

**To see how you might use dedupe with smallish data, see the [annotated source code for csv_example.py](http://datamade.github.com/dedupe-examples/docs/csv_example.html).**

### [Patent example](http://datamade.github.io/dedupe-examples/docs/patent_example.html) -  patent holders

This example works with Dutch inventors from the PATSTAT international patent data file

```bash
cd patent_example
pip install unidecode
python patent_example.py
```
  (use 'y', 'n' and 'u' keys to flag duplicates for active learning, 'f' when you are finished)

### [Record Linkage example](http://datamade.github.com/dedupe-examples/docs/record_linkage_example.html) -  electronics products
This example links two spreadsheets of electronics products and links up the matching entries. Each dataset individually has no duplicates.

```bash
cd record_linkage_example
python record_linkage_example.py
```

**To see how you might use dedupe for linking datasets, see the [annotated source code for record_linkage_example.py](http://datamade.github.com/dedupe-examples/docs/record_linkage_example.html).**

### [MySQL example](http://datamade.github.com/dedupe-examples/docs/mysql_example.html) - IL campaign contributions

See `mysql_example/README.md` for details

**To see how you might use dedupe with bigish data, see the [annotated source code for mysql_example](http://datamade.github.com/dedupe-examples/docs/mysql_example.html).**


### [PostgreSQL big dedupe example](http://datamade.github.io/dedupe-examples/docs/pgsql_big_dedupe_example.html) - PostgreSQL example on large dataset

See `pgsql_big_dedupe_example/README.md` for details

This is the same example as the MySQL IL campaign contributions dataset above, but ported to run on PostgreSQL.


## Training

The _secret sauce_ of dedupe is human input. In order to figure out the best rules to deduplicate a set of data, you must give it a set of labeled examples to learn from.

The more labeled examples you give it, the better the deduplication results will be. At minimum, you should try to provide __10 positive matches__ and __10 negative matches__.

The results of your training will be saved in a JSON file for future runs of dedupe.

Here's an example labeling operation:

```bash
Phone :  2850617
Address :  3801 s. wabash
Zip :
Site name :  ada s. mckinley st. thomas cdc

Phone :  2850617
Address :  3801 s wabash ave
Zip :
Site name :  ada s. mckinley community services - mckinley - st. thomas

Do these records refer to the same thing?
(y)es / (n)o / (u)nsure / (f)inished
```
