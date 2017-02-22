# Braavos-User-Guide-
User guide to use braavos from you local machine.
[official user guide](https://www.gitbook.com/book/ogre0403/nchc-braavos-user-guide)

## Using a Linux local machine

### Basic command

1. Remote access to your braavos instance

  ```
  ssh <username>@140.110.30.32 -p 22
  ```

2. Send files or folders from your local machine to yout braavos instance

  ```
  scp -P 22 <local_path> <username>@140.110.30.32:<path_on_braavos> 
  ```

### Set up iPython using PySpark

[link to the official user guide](https://ogre0403.gitbooks.io/nchc-braavos-user-guide/content/use_spark/ipython-notebook.html)

1. Create an iPython notebook profile named pyspark

  ```
  ipython profile create pyspark
  ```

2. Set up pysparck notebook profile 

  ```
  vim ~/.ipython/profile_pyspark/startup/00-pyspark-setup.py
  ```

  00-pyspark-setup.py

  ```python
  import os
  import sys
  spark_home = os.environ.get('SPARK_HOME', None)
  if not spark_home:
    raise ValueError('SPARK_HOME environment variable is not set')
  sys.path.insert(0, spark_home + "/python")
  sys.path.insert(0, os.path.join(spark_home, 'python/lib/py4j-0.8.2.1-src.zip'))
  execfile(os.path.join(spark_home, 'python/pyspark/shell.py'))
  ```

3. Start a notebook without starting a browser

  ```
  ipython notebook --profile=pyspark --no-browser --port=8889
  ```

4. Access to the notebook from your local machine

  (to run on your local machine)
  ```
  ssh -N -f -L localhost:8889:localhost:8889 <username>@140.110.30.32 -p 22
  ```
