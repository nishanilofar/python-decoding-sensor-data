# Decoding Data App

- [Decoding Data App](#decoding-data-app)
  - [Status](#status)
  - [Module 1: Load Sensor Data From Files](#module-1-load-sensor-data-from-files)
    - [Local verification instructions](#local-verification-instructions)
    - [M1: Task 1: Import os, glob, and csv](#m1-task-1-import-os-glob-and-csv)
    - [M1: Task 2: Create a Function to parse the data](#m1-task-2-create-a-function-to-parse-the-data)
    - [M1: Task 3: Sensor Data File Management](#m1-task-3-sensor-data-file-management)
    - [M1: Task 4: Read Data Files](#m1-task-4-read-data-files)
    - [M1: Task 5: Load Data Records](#m1-task-5-load-data-records)
    - [M1: Task 6: Get Sensor Data with sensor_app](#m1-task-6-get-sensor-data-with-sensorapp)

## Status

Draft.

## Module 1: Load Sensor Data From Files

In this first module, you will write a function to load the sensor data stored in the data files. The sensor data is stored in CSV files

### Local verification instructions

To test this module locally:

- Open a terminal at the root of the project
- Run the command `pytest -k module1`

### M1: Task 1: Import os, glob, and csv

[//]:# (@pytest.mark.test_load_data_import_module1)

The dataset for this project is stored in several CSV files found in the `dataset` folder. It represents the data from a device with multiple sensors. The data was collected at random times over a period of days. The records include measurements of temperature, humidity, energy consumption, and particle count in the air over a given area. The data is collected over a period of 24 hours.  

To start, open the file called `load_data.py` in the `sensor` folder.

At the top of the file, create three import statements for `os`, `glob`, and `csv`. These libraries will allow us to work with a collection of files.

### M1: Task 2: Create a Function to parse the data

[//]:# (@pytest.mark.test_load_data_load_sensor_func_module1)

Create a function called `load_sensor_data()` that has no parameters.
In the body of the `load_sensor_data()` function, create a variable called `sensor_data` and set it to an empty list.

### M1: Task 3: Sensor Data File Management

[//]:# (@pytest.mark.test_load_data_sensor_files_module1)

Next, create a variable called `sensor_files` that is set to a call to the `glob.glob()` function.

Pass the glob function a single argument, a call to the `os.path.join()` function.

In turn pass `os.path.join()` three arguments: `os.getcwd()`, `"datasets"`, and `"*.csv"`.

Your statement should look like this:

```python
    sensor_files = glob.glob(os.path.join(os.getcwd(), 'datasets', '*.csv'))
```

### M1: Task 4: Read Data Files

[//]:# (@pytest.mark.test_load_data_read_files_module1)

The `sensor_files` object contains a list of file names i.e. ['SENSOR_ROOM2', 'SENSOR_ROOM1']

To read the sensor data of these files, three steps are required:

1) Create one `for` loop that loops through `sensor_files` using `sensor_file` as the iterator variable.

2) In the body of this loop use a `with` statement to `open` the `sensor_file` and set the alias to `data_file`.

3) In the `with` body, set a variable called `data_reader` equal to `csv.DictReader()`. Pass in the current `data_file` as the first argument, and set the `delimiter=','` as the second argument. The `data_reader` will contain a list of ordered dictionaries with the sensor data records.

### M1: Task 5: Load Data Records

[//]:# (@pytest.mark.test_load_data_load_recs_module1)

Now that you have access to the data in each file, the next step is to load each record into the `sensor_data` list.

Within the `with`, create a second `for` loop to `data_file` to get access to each record. Use `row` as your iterator variable.

Inside the body of the second `for` loop, append each `row` record to the `sensor_data` list (you created this list earlier in the _Create a Function to Parse the Data_ task).

Finally, your function should return `sensor_data` (outside of all `for` loops, and the very end of the function).

### M1: Task 6: Get Sensor Data with sensor_app

[//]:# (@pytest.mark.test_sensor_app_load_data_return_module1)

Let's set up the command line interface (CLI). Open the `sensor_app.py` file in the `sensor` directory of the project.

At the top of the file, from the `load_data` module, `import` the `load_sensor_data` function.

Then, below the two initial lines of code provided in the file

```python
data = []
print("Sensor Data App")
```

Set the `data` list to `load_sensor_data()`.

Print the length of the `data` list using the [formatted string](https://docs.python.org/3/library/string.html#formatstrings) form  `str.format()`.

```python
print("Loaded records: {}".format(len(data)))
```

To preview your app, open a terminal at the root of the project and run the following command:

```bash
python sensor/sensor_app.py
```

Sample output:

```bash
Sensor Data App
Loaded records: 2000
```

Remember, each data file contains 1000 records.

FYI: the app will not validate your `print()` statements.

---
