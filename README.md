# caproto-archiver

This is a POC (proof of concept) application demonstrating that it's possible
to build an archiver application based on the Python package caproto, which
has the unique feature that it provides access to the binary representation
of the packages (i.e. datagrams) received via EPICS' Channel Access protocol.

## General Considerations

The idea of this POC is that the binary CA messages are the best way to
archive the state of EPICS process variables, as it is at the same time
very space efficient due to its packed binary format, and also there's no
data loss to be expected due to converting the values contained in the
CA datagrams to another format.

The downside could be slightly slower retrieval of large amounts of archived
data, as long as the parsing of the datagrams is implemented with caproto,
which is a Python-only library. For a fast response time, a C library or
similar would have to be used for this purpose. Would EPICS' libca.so be
able to fill the gap here? Remains to be determined.

## Running the caproto-archiver

The archiver uses the same configuration format as the CSS/RDB Archiver (aka *BEAUTY*).
An example configuration file is part of this repository.

By default, the archiver stores the archived data in the subfolder ./data/.

Start the archiver with:

```sh
./caproto_archiver.py --xml-config-file example_ioc.xml
```
