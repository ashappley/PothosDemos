# Custom C++ Type demo

A family of blocks may employ the use of custom data types as messages.
This demonstration shows how type registration and type serialization
can be used with a custom data type to cross process and language boundaries.

## Custom C++ Type FluffyData

Consider the custom type FluffyData. Using several variants of a simple
source and sink block, we can demonstrate how a registered type
can be interacted with using the Pothos::Proxy abstraction.

* FluffySource.cpp - produces FluffySource with the class definition
* FluffySource.cpp - produces FluffySource with the class registration
* FluffySink1.cpp - consumes and prints FluffySource with the class definition
* FluffySink2.cpp - consumes and prints FluffySource with the class registration
* FluffySource.py - produces FluffySource in python
* FluffySink.py - consumes and prints FluffySource in python

## Custom Python Type SpikeyData

Now consider a custom type SpikeyData which is defined in a Python module.
Python blocks can easily pass the type between themselves. However, through
the Pothos::Proxy abstraction, C++ blocks can just as easilyuse the type.

* SpikeySource.py - produces SpikeyData in python
* SpikeySink.py - consumes SpikeyData in python
* SpikeySource.cpp - produces SpikeyData in C++ through Proxy
* SpikeySink.cpp - consumes SpikeyData in C++ through Proxy

## Build the demo project

```
cd custom_types
mkdir build && cd build
cmake ../
make -j4
sudo make install
```

## Running test cases

A simple test runner script is provided to connect and run a pair of blocks.
Here are a few example test cases that show off the capabilities:

```
#Send FluffyData with the C++ source to the Python sink
python tester.py /demos/fluffy_source /demos/fluffy_sink_py

#Send FluffyData with the Python source to the C++ sink
python tester.py /demos/fluffy_source_py /demos/fluffy_sink

#Using proxy to manipulate FluffyData in C++ without class definitions
python tester.py /demos/fluffy_source2 /demos/fluffy_sink2

#Send SpikeyData with the C++ source to the Python sink
python tester.py /demos/spikey_source /demos/spikey_sink_py

#Send SpikeyData with the Python source to the C++ sink
python tester.py /demos/spikey_source_py /demos/spikey_sink
```