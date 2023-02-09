## Description :house:

AirBnB is a complete web application, integrating database storage, 
a back-end API, and front-end interfacing in a clone of AirBnB.

The project currently only implements the back-end console.

## Classes :cl:

AirBnB utilizes the following classes:

|     | BaseModel | FileStorage | User | State | City | Amenity | Place | Review |
| --- | --------- | ----------- | -----| ----- | -----| ------- | ----- | ------ |
| **PUBLIC INSTANCE ATTRIBUTES** | `id`<br>`created_at`<br>`updated_at` | | Inherits from `BaseModel` | Inherits from `BaseModel` | Inherits from `BaseModel` | Inherits from `BaseModel` | Inherits from `BaseModel` | Inherits from `BaseModel` |
| **PUBLIC INSTANCE METHODS** | `save`<br>`to_dict` | `all`<br>`new`<br>`save`<br>`reload` | "" | "" | "" | "" | "" | "" |
| **PUBLIC CLASS ATTRIBUTES** | | | `email`<br>`password`<br>`first_name`<br>`last_name`| `name` | `state_id`<br>`name` | `name` | `city_id`<br>`user_id`<br>`name`<br>`description`<br>`number_rooms`<br>`number_bathrooms`<br>`max_guest`<br>`price_by_night`<br>`latitude`<br>`longitude`<br>`amenity_ids` | `place_id`<br>`user_id`<br>`text` | 
| **PRIVATE CLASS ATTRIBUTES** | | `file_path`<br>`objects` | | | | | | |

## Storage :baggage claim:

The above classes are handled by the abstracted storage engine defined in the 
[FileStorage](./models/engine/file_storage.py) class.

Every time the backend is initialized, AirBnB instantiates an instance of 
`FileStorage` called `storage`. The `storage` object is loaded/re-loaded from 
any class instances stored in the JSON file `file.json`. As class instances are 
created, updated, or deleted, the `storage` object is used to register 
corresponding changes in the `file.json`.

## Console :computer:

The console is a command line interpreter that permits management of the backend 
of AirBnB. It can be used to handle and manipulate all classes utilized by 
the application (achieved by calls on the `storage` object defined above).

### Using the Console

The AirBnB console can be run both interactively and non-interactively. 
To run the console in non-interactive mode, pipe any command(s) into an execution 
of the file `console.py` at the command line.

```
$ echo "help" | ./console.py
(abnb) 
Documented commands (type help <topic>):
========================================
EOF  all  count  create  destroy  help  quit  show  update

(abnb) 
$
```

Alternatively, to use the Airbnb console in interactive mode, run the 
file `console.py` by itself:

```
$ ./console.py
```

While running in interactive mode, the console displays a prompt for input:

```
$ ./console.py
(abnb) 
```

To quit the console, enter the command `quit`, or input an EOF signal 
(`ctrl-D`).

```
$ ./console.py
(abnb) quit
$
```

```
$ ./console.py
(abnb) EOF
$
```

### Console Commands

The Airbnb console supports the following commands:

* **create**
  * Usage: `create <class>`

Creates a new instance of a given class. The class' ID is printed and 
the instance is saved to the file `file.json`.

```
$ ./console.py
(abnb) create BaseModel
119be863-6fe5-437e-a180-b9892e8746b8
(abnb) quit
$ cat file.json ; echo ""
```

* **show**
  * Usage: `show <class> <id>` or `<class>.show(<id>)`

Prints the string representation of a class instance based on a given id.

```
$ ./console.py
(abnb) create User
1e32232d-5a63-4d92-8092-ac3240b29f46
(abnb)
(abnb) show User
```
* **destroy**
  * Usage: `destroy <class> <id>` or `<class>.destroy(<id>)`

Deletes a class instance based on a given id. The storage file `file.json` 
is updated accordingly.

```
$ ./console.py
(abnb) create State
d2d789cd-7427-4920-aaae-88cbcf8bffe2
(abnb) create Place
3e-8329-4f47-9947-dca80c03d3ed
(abnb)
(abnb) destroy State d2d789cd-7427-4920-aaae-88cbcf8bffe2
(abnb) Place.destroy(03486a3e-8329-4f47-9947-dca80c03d3ed)
(abnb) quit
$ cat file.json ; echo ""
{}
```

* **all**
  * Usage: `all` or `all <class>` or `<class>.all()`

Prints the string representations of all instances of a given class. If no 
class name is provided, the command prints all instances of every class.

```
$ ./console.py
(abnb) create BaseModel
fce2124c-8537-489b-956e-22da455cbee8
(abnb) create BaseModel
450490fd-344e-47cf-8342-126244c2ba99
(abnb) create User
b742dbc3-f4bf-425e-b1d4-165f52c6ff81
(abnb) create User
8f2d75c8-fb82-48e1-8ae5-2544c909a9fe
(abnb) 
```

* **count**
  * Usage: `count <class>` or `<class>.count()`

Retrieves the number of instances of a given class.

```
$ ./console.py
(abnb) create Place
12c73223-f3d3-4dec-9629-bd19c8fadd8a
(abnb) create Place
aa229cbb-5b19-4c32-8562-f90a3437d301
(abnb) create City
22a51611-17bd-4d8f-ba1b-3bf07d327208
(abnb) 
(abnb) count Place
2
(abnb) city.count()
1
(abnb) 
```

* **update**
  * Usage: `update <class> <id> <attribute name> "<attribute value>"` or
`<class>.update(<id>, <attribute name>, <attribute value>)` or `<class>.update(
<id>, <attribute dictionary>)`.

Updates a class instance based on a given id with a given key/value attribute 
pair or dictionary of attribute pairs. If `update` is called with a single 
key/value attribute pair, only "simple" attributes can be updated (ie. not 
`id`, `created_at`, and `updated_at`). However, any attribute can be updated by 
providing a dictionary.

```
$ ./console.py
(abnb) create User
6f348019-0499-420f-8eec-ef0fdc863c02
(abnb)
```

## Testing :straight ruler:

Unittests for the project are defined in the [tests](./tests) 
folder. To run the entire test suite simultaneously, execute the following command:

```
$ python3 unittest -m discover tests
```

Alternatively, you can specify a single test file to run at a time:

```
$ python3 unittest -m tests/test console.py
```

## Authors :black nib:
* *Felix Odhiambo** <[felix](https://github.com/fellohodhis)>
